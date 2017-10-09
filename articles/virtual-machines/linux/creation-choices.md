---
title: aaaDifferent modi toocreate una VM Linux di Azure | Microsoft Azure
description: Informazioni su modi diversi di hello toocreate una macchina virtuale di Linux in Azure, inclusi i collegamenti tootools ed esercitazioni per ogni metodo.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a><span data-ttu-id="40c4d-103">Modi diversi toocreate una VM Linux</span><span class="sxs-lookup"><span data-stu-id="40c4d-103">Different ways toocreate a Linux VM</span></span>
<span data-ttu-id="40c4d-104">È la flessibilità di hello in Azure toocreate una macchina virtuale Linux (VM) tooyou preferisci strumenti e i flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="40c4d-104">You have hello flexibility in Azure toocreate a Linux virtual machine (VM) using tools and workflows comfortable tooyou.</span></span> <span data-ttu-id="40c4d-105">In questo articolo riepiloga le differenze e gli esempi per creare le macchine virtuali Linux, tra cui hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="40c4d-105">This article summarizes these differences and examples for creating your Linux VMs, including hello Azure CLI 2.0.</span></span> <span data-ttu-id="40c4d-106">È inoltre possibile visualizzare le opzioni di creazione inclusi hello [CLI di Azure 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="40c4d-106">You can also view creation choices including hello [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="40c4d-107">Hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) è disponibile tra le piattaforme tramite un pacchetto npm, pacchetti di distribuzione fornito o contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="40c4d-107">hello [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="40c4d-108">Installare hello build più appropriato per l'ambiente e accedere con un account Azure tooan [accesso az](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="40c4d-108">Install hello most appropriate build for your environment and log in tooan Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="40c4d-109">Creare una VM Linux con hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="40c4d-109">Create a Linux VM with hello Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="40c4d-110">Usare [az group create](/cli/azure/group#create) per creare un gruppo di risorse denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="40c4d-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="40c4d-111">Creare una macchina virtuale con [creare vm az](/cli/azure/vm#create) denominato *myVM* utilizzando hello più recente *UbuntuLTS* immagine e generare le chiavi SSH se sono già presenti *~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="40c4d-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using hello latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="40c4d-112">Creare una VM Linux con un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="40c4d-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="40c4d-113">Hello seguente utilizza [distribuzione gruppo az creare](/cli/azure/group/deployment#create) toocreate una macchina virtuale da un modello archiviato in GitHub:</span><span class="sxs-lookup"><span data-stu-id="40c4d-113">hello following example uses [az group deployment create](/cli/azure/group/deployment#create) toocreate a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="40c4d-114">Creare una VM Linux e personalizzarla con cloud-init</span><span class="sxs-lookup"><span data-stu-id="40c4d-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="40c4d-115">Creare un'applicazione con carico bilanciato e disponibilità elevata in più VM Linux</span><span class="sxs-lookup"><span data-stu-id="40c4d-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="40c4d-116">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="40c4d-116">Azure portal</span></span>
<span data-ttu-id="40c4d-117">Hello [portale di Azure](https://portal.azure.com) consente tooquickly creare una macchina virtuale poiché non c'è niente tooinstall nel sistema.</span><span class="sxs-lookup"><span data-stu-id="40c4d-117">hello [Azure portal](https://portal.azure.com) allows you tooquickly create a VM since there is nothing tooinstall on your system.</span></span> <span data-ttu-id="40c4d-118">Utilizzare hello toocreate portale Azure hello VM:</span><span class="sxs-lookup"><span data-stu-id="40c4d-118">Use hello Azure portal toocreate hello VM:</span></span>

* [<span data-ttu-id="40c4d-119">Creare una VM Linux di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="40c4d-119">Create a Linux VM using hello Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="40c4d-120">Sistema operativo e opzioni dell'immagine</span><span class="sxs-lookup"><span data-stu-id="40c4d-120">Operating system and image choices</span></span>
<span data-ttu-id="40c4d-121">Quando si crea una macchina virtuale, si sceglie un'immagine in base a hello desiderato toorun sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="40c4d-121">When creating a VM, you choose an image based on hello operating system you want toorun.</span></span> <span data-ttu-id="40c4d-122">Azure e i relativi partner mettono a disposizione diverse immagini, alcune delle quali includono applicazioni e strumenti preinstallati.</span><span class="sxs-lookup"><span data-stu-id="40c4d-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="40c4d-123">O, caricare una delle proprie immagini (vedere [hello seguente sezione](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="40c4d-123">Or, upload one of your own images (see [hello following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="40c4d-124">Immagini di Azure</span><span class="sxs-lookup"><span data-stu-id="40c4d-124">Azure images</span></span>
<span data-ttu-id="40c4d-125">Hello utilizzare [immagine di macchina virtuale az](/cli/azure/vm/image) comandi toosee disponibili dal server di pubblicazione, versione di distribuzione e le compilazioni.</span><span class="sxs-lookup"><span data-stu-id="40c4d-125">Use hello [az vm image](/cli/azure/vm/image) commands toosee what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="40c4d-126">Elenca gli editori disponibili:</span><span class="sxs-lookup"><span data-stu-id="40c4d-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="40c4d-127">Elenca i prodotti disponibili (offerte) per un determinato editore:</span><span class="sxs-lookup"><span data-stu-id="40c4d-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="40c4d-128">Elenca gli SKU disponibili (versioni di distribuzione) di una determinata offerta:</span><span class="sxs-lookup"><span data-stu-id="40c4d-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="40c4d-129">Elenca tutte le immagini disponibili per una determinata versione:</span><span class="sxs-lookup"><span data-stu-id="40c4d-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="40c4d-130">Per ulteriori esempi sull'esplorazione e l'utilizzo di immagini disponibili, vedere [Naviga e selezionare le immagini di macchina virtuale di Azure con hello Azure CLI](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="40c4d-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with hello Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="40c4d-131">Hello [creare vm az](/cli/azure/vm#create) comando dispone di alias è possibile usare accesso tooquickly hello distribuzioni più comuni e le versioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="40c4d-131">hello [az vm create](/cli/azure/vm#create) command has aliases you can use tooquickly access hello more common distros and their latest releases.</span></span> <span data-ttu-id="40c4d-132">Utilizzo degli alias è spesso più veloce rispetto all'impostazione publisher hello, offerta, SKU e versione ogni volta che si crea una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="40c4d-132">Using aliases is often quicker than specifying hello publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="40c4d-133">Alias</span><span class="sxs-lookup"><span data-stu-id="40c4d-133">Alias</span></span> | <span data-ttu-id="40c4d-134">Autore</span><span class="sxs-lookup"><span data-stu-id="40c4d-134">Publisher</span></span> | <span data-ttu-id="40c4d-135">Offerta</span><span class="sxs-lookup"><span data-stu-id="40c4d-135">Offer</span></span> | <span data-ttu-id="40c4d-136">SKU</span><span class="sxs-lookup"><span data-stu-id="40c4d-136">SKU</span></span> | <span data-ttu-id="40c4d-137">Versione</span><span class="sxs-lookup"><span data-stu-id="40c4d-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="40c4d-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="40c4d-138">CentOS</span></span> |<span data-ttu-id="40c4d-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="40c4d-139">OpenLogic</span></span> |<span data-ttu-id="40c4d-140">Centos</span><span class="sxs-lookup"><span data-stu-id="40c4d-140">Centos</span></span> |<span data-ttu-id="40c4d-141">7,2</span><span class="sxs-lookup"><span data-stu-id="40c4d-141">7.2</span></span> |<span data-ttu-id="40c4d-142">più recenti</span><span class="sxs-lookup"><span data-stu-id="40c4d-142">latest</span></span> |
| <span data-ttu-id="40c4d-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="40c4d-143">CoreOS</span></span> |<span data-ttu-id="40c4d-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="40c4d-144">CoreOS</span></span> |<span data-ttu-id="40c4d-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="40c4d-145">CoreOS</span></span> |<span data-ttu-id="40c4d-146">Stabile</span><span class="sxs-lookup"><span data-stu-id="40c4d-146">Stable</span></span> |<span data-ttu-id="40c4d-147">più recenti</span><span class="sxs-lookup"><span data-stu-id="40c4d-147">latest</span></span> |
| <span data-ttu-id="40c4d-148">Debian</span><span class="sxs-lookup"><span data-stu-id="40c4d-148">Debian</span></span> |<span data-ttu-id="40c4d-149">credativ</span><span class="sxs-lookup"><span data-stu-id="40c4d-149">credativ</span></span> |<span data-ttu-id="40c4d-150">Debian</span><span class="sxs-lookup"><span data-stu-id="40c4d-150">Debian</span></span> |<span data-ttu-id="40c4d-151">8</span><span class="sxs-lookup"><span data-stu-id="40c4d-151">8</span></span> |<span data-ttu-id="40c4d-152">più recenti</span><span class="sxs-lookup"><span data-stu-id="40c4d-152">latest</span></span> |
| <span data-ttu-id="40c4d-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="40c4d-153">openSUSE</span></span> |<span data-ttu-id="40c4d-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="40c4d-154">SUSE</span></span> |<span data-ttu-id="40c4d-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="40c4d-155">openSUSE</span></span> |<span data-ttu-id="40c4d-156">13.2</span><span class="sxs-lookup"><span data-stu-id="40c4d-156">13.2</span></span> |<span data-ttu-id="40c4d-157">più recenti</span><span class="sxs-lookup"><span data-stu-id="40c4d-157">latest</span></span> |
| <span data-ttu-id="40c4d-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="40c4d-158">RHEL</span></span> |<span data-ttu-id="40c4d-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="40c4d-159">Redhat</span></span> |<span data-ttu-id="40c4d-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="40c4d-160">RHEL</span></span> |<span data-ttu-id="40c4d-161">7,2</span><span class="sxs-lookup"><span data-stu-id="40c4d-161">7.2</span></span> |<span data-ttu-id="40c4d-162">più recenti</span><span class="sxs-lookup"><span data-stu-id="40c4d-162">latest</span></span> |
| <span data-ttu-id="40c4d-163">SLES</span><span class="sxs-lookup"><span data-stu-id="40c4d-163">SLES</span></span> |<span data-ttu-id="40c4d-164">SLES</span><span class="sxs-lookup"><span data-stu-id="40c4d-164">SLES</span></span> |<span data-ttu-id="40c4d-165">SLES</span><span class="sxs-lookup"><span data-stu-id="40c4d-165">SLES</span></span> |<span data-ttu-id="40c4d-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="40c4d-166">12-SP1</span></span> |<span data-ttu-id="40c4d-167">più recenti</span><span class="sxs-lookup"><span data-stu-id="40c4d-167">latest</span></span> |
| <span data-ttu-id="40c4d-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="40c4d-168">UbuntuLTS</span></span> |<span data-ttu-id="40c4d-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="40c4d-169">Canonical</span></span> |<span data-ttu-id="40c4d-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="40c4d-170">UbuntuServer</span></span> |<span data-ttu-id="40c4d-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="40c4d-171">14.04.4-LTS</span></span> |<span data-ttu-id="40c4d-172">più recenti</span><span class="sxs-lookup"><span data-stu-id="40c4d-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="40c4d-173">Usare la propria immagine</span><span class="sxs-lookup"><span data-stu-id="40c4d-173">Use your own image</span></span>
<span data-ttu-id="40c4d-174">Per personalizzazioni specifiche è possibile usare un'immagine basata su una VM di Azure esistente acquisendo tale VM.</span><span class="sxs-lookup"><span data-stu-id="40c4d-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="40c4d-175">È anche possibile caricare un'immagine creata in locale.</span><span class="sxs-lookup"><span data-stu-id="40c4d-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="40c4d-176">Per ulteriori informazioni sulle distribuzioni supportate e come toouse immagini personalizzate, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="40c4d-176">For more information on supported distros and how toouse your own images, see hello following articles:</span></span>

* [<span data-ttu-id="40c4d-177">Distribuzioni approvate per Azure</span><span class="sxs-lookup"><span data-stu-id="40c4d-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="40c4d-178">Informazioni per distribuzioni non approvate</span><span class="sxs-lookup"><span data-stu-id="40c4d-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="40c4d-179">[Come un'immagine da una macchina virtuale di Azure esistente toocreate](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="40c4d-179">[How toocreate an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="40c4d-180">Guida introduttiva all'esempio comandi toocreate un'immagine da una macchina virtuale di Azure esistente:</span><span class="sxs-lookup"><span data-stu-id="40c4d-180">Quick-start example commands toocreate an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="40c4d-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="40c4d-181">Next steps</span></span>
* <span data-ttu-id="40c4d-182">Creare una VM Linux con hello [CLI](quick-create-cli.md), da hello [portale](quick-create-portal.md), o tramite un [modello di Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="40c4d-182">Create a Linux VM with hello [CLI](quick-create-cli.md), from hello [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="40c4d-183">Dopo aver creato una VM Linux, vedere le [informazioni sui dischi e l'archiviazione di Azure](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="40c4d-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="40c4d-184">I passaggi troppo veloce[reimpostare una password o le chiavi SSH e gestire gli utenti](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="40c4d-184">Quick steps too[reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
