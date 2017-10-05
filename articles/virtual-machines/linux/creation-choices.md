---
title: Diversi modi per creare una macchina virtuale Linux in Azure | Microsoft Azure
description: Informazioni sui diversi modi per creare una macchina virtuale Linux in Azure, con collegamenti a strumenti ed esercitazioni per ogni metodo.
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
ms.openlocfilehash: b2f93579eb1c7a69d0dbd1b0ef112aed9b2168c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-linux-vm"></a><span data-ttu-id="4c346-103">Diversi modi di creare una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="4c346-103">Different ways to create a Linux VM</span></span>
<span data-ttu-id="4c346-104">Azure offre la possibilità di creare una macchina virtuale (VM) Linux usando gli strumenti e i flussi di lavoro con cui si ha familiarità.</span><span class="sxs-lookup"><span data-stu-id="4c346-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="4c346-105">Questo articolo offre un riepilogo delle differenze e degli esempi per la creazione di VM Linux e include l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="4c346-105">This article summarizes these differences and examples for creating your Linux VMs, including the Azure CLI 2.0.</span></span> <span data-ttu-id="4c346-106">È inoltre possibile visualizzare le opzioni tra cui l'[interfaccia della riga di comando di Azure 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4c346-106">You can also view creation choices including the [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="4c346-107">L'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) è disponibile per più piattaforme tramite un pacchetto npm, pacchetti forniti tramite distribuzione o un contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="4c346-107">The [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="4c346-108">Installare la build più appropriata per l'ambiente e accedere a un account Azure usando [az login](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="4c346-108">Install the most appropriate build for your environment and log in to an Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="4c346-109">Creare una VM Linux con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4c346-109">Create a Linux VM with the Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="4c346-110">Usare [az group create](/cli/azure/group#create) per creare un gruppo di risorse denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="4c346-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="4c346-111">Usare [az vm create](/cli/azure/vm#create) per creare una VM denominata *myVM* tramite l'immagine *UbuntuLTS* più recente e generare chiavi SSH se non sono già presenti in *~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="4c346-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using the latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="4c346-112">Creare una VM Linux con un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="4c346-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="4c346-113">L'esempio seguente usa [az group deployment create](/cli/azure/group/deployment#create) per creare una VM da un modello archiviato in GitHub:</span><span class="sxs-lookup"><span data-stu-id="4c346-113">The following example uses [az group deployment create](/cli/azure/group/deployment#create) to create a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="4c346-114">Creare una VM Linux e personalizzarla con cloud-init</span><span class="sxs-lookup"><span data-stu-id="4c346-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="4c346-115">Creare un'applicazione con carico bilanciato e disponibilità elevata in più VM Linux</span><span class="sxs-lookup"><span data-stu-id="4c346-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="4c346-116">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4c346-116">Azure portal</span></span>
<span data-ttu-id="4c346-117">Il [portale di Azure](https://portal.azure.com) consente di creare rapidamente una VM perché non richiede installazioni nel sistema.</span><span class="sxs-lookup"><span data-stu-id="4c346-117">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="4c346-118">Usare il portale di Azure per creare la VM:</span><span class="sxs-lookup"><span data-stu-id="4c346-118">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="4c346-119">Creare una macchina virtuale Linux tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4c346-119">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="4c346-120">Sistema operativo e opzioni dell'immagine</span><span class="sxs-lookup"><span data-stu-id="4c346-120">Operating system and image choices</span></span>
<span data-ttu-id="4c346-121">Quando si crea una macchina virtuale, scegliere un'immagine in base al sistema operativo da eseguire.</span><span class="sxs-lookup"><span data-stu-id="4c346-121">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="4c346-122">Azure e i relativi partner mettono a disposizione diverse immagini, alcune delle quali includono applicazioni e strumenti preinstallati.</span><span class="sxs-lookup"><span data-stu-id="4c346-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="4c346-123">In alternativa, caricare una delle immagini personalizzate (vedere la [sezione seguente](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="4c346-123">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="4c346-124">Immagini di Azure</span><span class="sxs-lookup"><span data-stu-id="4c346-124">Azure images</span></span>
<span data-ttu-id="4c346-125">Usare i comandi [az vm image](/cli/azure/vm/image) per visualizzare ciò che è disponibile per editore, versione di distribuzione e build.</span><span class="sxs-lookup"><span data-stu-id="4c346-125">Use the [az vm image](/cli/azure/vm/image) commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="4c346-126">Elenca gli editori disponibili:</span><span class="sxs-lookup"><span data-stu-id="4c346-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="4c346-127">Elenca i prodotti disponibili (offerte) per un determinato editore:</span><span class="sxs-lookup"><span data-stu-id="4c346-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="4c346-128">Elenca gli SKU disponibili (versioni di distribuzione) di una determinata offerta:</span><span class="sxs-lookup"><span data-stu-id="4c346-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="4c346-129">Elenca tutte le immagini disponibili per una determinata versione:</span><span class="sxs-lookup"><span data-stu-id="4c346-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="4c346-130">Per altri esempi sull'esplorazione e l'uso delle immagini disponibili, vedere [Individuare e selezionare immagini di macchine virtuali di Azure con l'interfaccia della riga di comando di Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="4c346-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with the Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="4c346-131">Il comando [az vm create](/cli/azure/vm#create) ha alias che è possibile usare per accedere rapidamente alle distribuzioni più comuni e alle versioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="4c346-131">The [az vm create](/cli/azure/vm#create) command has aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="4c346-132">Usare alias è in genere più veloce che specificare editore, offerta, SKU e versione ogni volta che si crea una VM:</span><span class="sxs-lookup"><span data-stu-id="4c346-132">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="4c346-133">Alias</span><span class="sxs-lookup"><span data-stu-id="4c346-133">Alias</span></span> | <span data-ttu-id="4c346-134">Autore</span><span class="sxs-lookup"><span data-stu-id="4c346-134">Publisher</span></span> | <span data-ttu-id="4c346-135">Offerta</span><span class="sxs-lookup"><span data-stu-id="4c346-135">Offer</span></span> | <span data-ttu-id="4c346-136">SKU</span><span class="sxs-lookup"><span data-stu-id="4c346-136">SKU</span></span> | <span data-ttu-id="4c346-137">Versione</span><span class="sxs-lookup"><span data-stu-id="4c346-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="4c346-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="4c346-138">CentOS</span></span> |<span data-ttu-id="4c346-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="4c346-139">OpenLogic</span></span> |<span data-ttu-id="4c346-140">Centos</span><span class="sxs-lookup"><span data-stu-id="4c346-140">Centos</span></span> |<span data-ttu-id="4c346-141">7,2</span><span class="sxs-lookup"><span data-stu-id="4c346-141">7.2</span></span> |<span data-ttu-id="4c346-142">più recenti</span><span class="sxs-lookup"><span data-stu-id="4c346-142">latest</span></span> |
| <span data-ttu-id="4c346-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="4c346-143">CoreOS</span></span> |<span data-ttu-id="4c346-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="4c346-144">CoreOS</span></span> |<span data-ttu-id="4c346-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="4c346-145">CoreOS</span></span> |<span data-ttu-id="4c346-146">Stabile</span><span class="sxs-lookup"><span data-stu-id="4c346-146">Stable</span></span> |<span data-ttu-id="4c346-147">più recenti</span><span class="sxs-lookup"><span data-stu-id="4c346-147">latest</span></span> |
| <span data-ttu-id="4c346-148">Debian</span><span class="sxs-lookup"><span data-stu-id="4c346-148">Debian</span></span> |<span data-ttu-id="4c346-149">credativ</span><span class="sxs-lookup"><span data-stu-id="4c346-149">credativ</span></span> |<span data-ttu-id="4c346-150">Debian</span><span class="sxs-lookup"><span data-stu-id="4c346-150">Debian</span></span> |<span data-ttu-id="4c346-151">8</span><span class="sxs-lookup"><span data-stu-id="4c346-151">8</span></span> |<span data-ttu-id="4c346-152">più recenti</span><span class="sxs-lookup"><span data-stu-id="4c346-152">latest</span></span> |
| <span data-ttu-id="4c346-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="4c346-153">openSUSE</span></span> |<span data-ttu-id="4c346-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="4c346-154">SUSE</span></span> |<span data-ttu-id="4c346-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="4c346-155">openSUSE</span></span> |<span data-ttu-id="4c346-156">13.2</span><span class="sxs-lookup"><span data-stu-id="4c346-156">13.2</span></span> |<span data-ttu-id="4c346-157">più recenti</span><span class="sxs-lookup"><span data-stu-id="4c346-157">latest</span></span> |
| <span data-ttu-id="4c346-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="4c346-158">RHEL</span></span> |<span data-ttu-id="4c346-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="4c346-159">Redhat</span></span> |<span data-ttu-id="4c346-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="4c346-160">RHEL</span></span> |<span data-ttu-id="4c346-161">7,2</span><span class="sxs-lookup"><span data-stu-id="4c346-161">7.2</span></span> |<span data-ttu-id="4c346-162">più recenti</span><span class="sxs-lookup"><span data-stu-id="4c346-162">latest</span></span> |
| <span data-ttu-id="4c346-163">SLES</span><span class="sxs-lookup"><span data-stu-id="4c346-163">SLES</span></span> |<span data-ttu-id="4c346-164">SLES</span><span class="sxs-lookup"><span data-stu-id="4c346-164">SLES</span></span> |<span data-ttu-id="4c346-165">SLES</span><span class="sxs-lookup"><span data-stu-id="4c346-165">SLES</span></span> |<span data-ttu-id="4c346-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="4c346-166">12-SP1</span></span> |<span data-ttu-id="4c346-167">più recenti</span><span class="sxs-lookup"><span data-stu-id="4c346-167">latest</span></span> |
| <span data-ttu-id="4c346-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="4c346-168">UbuntuLTS</span></span> |<span data-ttu-id="4c346-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="4c346-169">Canonical</span></span> |<span data-ttu-id="4c346-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="4c346-170">UbuntuServer</span></span> |<span data-ttu-id="4c346-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="4c346-171">14.04.4-LTS</span></span> |<span data-ttu-id="4c346-172">più recenti</span><span class="sxs-lookup"><span data-stu-id="4c346-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="4c346-173">Usare la propria immagine</span><span class="sxs-lookup"><span data-stu-id="4c346-173">Use your own image</span></span>
<span data-ttu-id="4c346-174">Per personalizzazioni specifiche è possibile usare un'immagine basata su una VM di Azure esistente acquisendo tale VM.</span><span class="sxs-lookup"><span data-stu-id="4c346-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="4c346-175">È anche possibile caricare un'immagine creata in locale.</span><span class="sxs-lookup"><span data-stu-id="4c346-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="4c346-176">Per altre informazioni sulle distribuzioni supportate e su come usare immagini personalizzate, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c346-176">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="4c346-177">Distribuzioni approvate per Azure</span><span class="sxs-lookup"><span data-stu-id="4c346-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="4c346-178">Informazioni per distribuzioni non approvate</span><span class="sxs-lookup"><span data-stu-id="4c346-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="4c346-179">[Come creare un'immagine da una VM di Azure esistente](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="4c346-179">[How to create an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="4c346-180">Comandi di esempio di avvio rapido per la creazione di un'immagine da una VM di Azure esistente:</span><span class="sxs-lookup"><span data-stu-id="4c346-180">Quick-start example commands to create an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="4c346-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4c346-181">Next steps</span></span>
* <span data-ttu-id="4c346-182">Creare una VM Linux con l'[interfaccia della riga di comando](quick-create-cli.md), il [portale di Azure](quick-create-portal.md) o un [modello di Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4c346-182">Create a Linux VM with the [CLI](quick-create-cli.md), from the [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="4c346-183">Dopo aver creato una VM Linux, vedere le [informazioni sui dischi e l'archiviazione di Azure](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="4c346-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="4c346-184">Azioni rapide per [reimpostare una password o chiavi SSH e gestire gli utenti](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="4c346-184">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
