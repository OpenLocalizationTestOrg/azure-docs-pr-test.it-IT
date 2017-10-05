---
title: Diversi modi per creare una VM Linux con l'Interfaccia della riga di comando di Azure 1.0 | Microsoft Docs
description: Informazioni sui diversi modi per creare una macchina virtuale Linux in Azure, con collegamenti a strumenti ed esercitazioni per ogni metodo.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 1eb90d44797d66f3e09811918ce5a7f4ad4287c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="3cb9c-103">Diversi modi per creare una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="3cb9c-103">Different ways to create a Linux virtual machine in Azure</span></span>
<span data-ttu-id="3cb9c-104">Azure offre la possibilità di creare una macchina virtuale (VM) Linux usando gli strumenti e i flussi di lavoro con cui si ha familiarità.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="3cb9c-105">Questo articolo offre un riepilogo delle differenze e degli esempi per la creazione di VM Linux.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-105">This article summarizes these differences and examples for creating your Linux VMs.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="3cb9c-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3cb9c-106">Azure CLI</span></span>
<span data-ttu-id="3cb9c-107">È possibile creare macchine virtuali in Azure usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-107">You can create VMs in Azure using one of the following CLI versions:</span></span>

- <span data-ttu-id="3cb9c-108">Interfaccia della riga di comando di Azure 1.0: interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="3cb9c-108">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="3cb9c-109">[Interfaccia della riga di comando di Azure 2.0](../windows/creation-choices.md): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="3cb9c-109">[Azure CLI 2.0](../windows/creation-choices.md) - our next generation CLI for the resource management deployment model</span></span>

<span data-ttu-id="3cb9c-110">L'interfaccia della riga di comando di Azure 1.0 è disponibile per più piattaforme tramite un pacchetto npm, pacchetti forniti tramite distribuzione o un contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-110">The Azure CLI 1.0 is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="3cb9c-111">Altre informazioni su come [Installare l'interfaccia della riga di comando di Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3cb9c-111">You can read more about [how to install and configure the Azure CLI](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="3cb9c-112">Le esercitazioni seguenti offrono esempi relativi all'uso dell'interfaccia della riga di comando di Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-112">The following tutorials provide examples on using the Azure CLI 1.0.</span></span> <span data-ttu-id="3cb9c-113">Vedere ogni articolo per altre informazioni sui comandi di avvio rapido dell'interfaccia della riga di comando illustrati:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-113">Read each article for more details on the CLI quick-start commands shown:</span></span>

* [<span data-ttu-id="3cb9c-114">Creare una VM Linux dall'interfaccia della riga di comando di Azure per sviluppo e test</span><span class="sxs-lookup"><span data-stu-id="3cb9c-114">Create a Linux VM from the Azure CLI for dev and test</span></span>](quick-create-cli-nodejs.md)
  
  * <span data-ttu-id="3cb9c-115">L'esempio seguente crea una VM CoreOS usando una chiave pubblica denominata *azure_id_rsa.pub*:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-115">The following example creates a CoreOS VM using a public key named *azure_id_rsa.pub*:</span></span>
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [<span data-ttu-id="3cb9c-116">Creare una VM Linux protetta usando un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="3cb9c-116">Create a secured Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="3cb9c-117">L'esempio seguente crea una VM usando un modello archiviato in GitHub:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-117">The following example creates a VM using a template stored on GitHub:</span></span>
    
    ```azurecli
    azure group create --name myResourceGroup --location eastus 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [<span data-ttu-id="3cb9c-118">Creare un ambiente Linux completo tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3cb9c-118">Create a complete Linux environment using the Azure CLI</span></span>](create-cli-complete-nodejs.md)
  
  * <span data-ttu-id="3cb9c-119">Include la creazione di un servizio di bilanciamento del carico e di più VM in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-119">Includes creating a load balancer and multiple VMs in an availability set.</span></span>
* [<span data-ttu-id="3cb9c-120">Aggiungere un disco a una VM Linux</span><span class="sxs-lookup"><span data-stu-id="3cb9c-120">Add a disk to a Linux VM</span></span>](add-disk.md)
  
  * <span data-ttu-id="3cb9c-121">L'esempio seguente aggiunge un disco da *5* GB a una VM esistente denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-121">The following example adds a *5* Gb disk to an existing VM named *myVM*:</span></span>
    
    ```azurecli
    azure vm disk attach-new \
        --resource-group myResourceGroup \
        --vm-name myVM \
        --size-in-GB 5
    ```

## <a name="azure-portal"></a><span data-ttu-id="3cb9c-122">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3cb9c-122">Azure portal</span></span>
<span data-ttu-id="3cb9c-123">Il [portale di Azure](https://portal.azure.com) consente di creare rapidamente una VM perché non richiede installazioni nel sistema.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-123">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="3cb9c-124">Usare il portale di Azure per creare la VM:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-124">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="3cb9c-125">Creare una macchina virtuale Linux tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3cb9c-125">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 

## <a name="operating-system-and-image-choices"></a><span data-ttu-id="3cb9c-126">Sistema operativo e opzioni dell'immagine</span><span class="sxs-lookup"><span data-stu-id="3cb9c-126">Operating system and image choices</span></span>
<span data-ttu-id="3cb9c-127">Quando si crea una macchina virtuale, scegliere un'immagine in base al sistema operativo da eseguire.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-127">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="3cb9c-128">Azure e i relativi partner mettono a disposizione diverse immagini, alcune delle quali includono applicazioni e strumenti preinstallati.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-128">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="3cb9c-129">In alternativa, caricare una delle immagini personalizzate (vedere la [sezione seguente](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="3cb9c-129">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="3cb9c-130">Immagini di Azure</span><span class="sxs-lookup"><span data-stu-id="3cb9c-130">Azure images</span></span>
<span data-ttu-id="3cb9c-131">Usare i comandi dell'interfaccia della riga di comando `azure vm image` per visualizzare ciò che è disponibile per editore, versione di distribuzione e build.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-131">Use the `azure vm image` CLI commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="3cb9c-132">Elencare gli editori disponibili come segue:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-132">List available publishers as follows:</span></span>

```azurecli
azure vm image list-publishers --location eastus
```

<span data-ttu-id="3cb9c-133">Elencare i prodotti disponibili (offerte) per un determinato editore come segue:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-133">List available products (offers) for a given publisher as follows:</span></span>

```azurecli
azure vm image list-offers --location eastus --publisher Canonical
```

<span data-ttu-id="3cb9c-134">Elencare gli SKU disponibili (versioni di distribuzione) di una determinata offerta come segue:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-134">List available SKUs (distro releases) of a given offer as follows:</span></span>

```azurecli
azure vm image list-skus --location eastus --publisher Canonical --offer UbuntuServer
```

<span data-ttu-id="3cb9c-135">Elencare tutte le immagini disponibili per una determinata versione come segue:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-135">List all available images for a given release follows:</span></span>

```azurecli
azure vm image list --location eastus --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

<span data-ttu-id="3cb9c-136">I comandi `azure vm quick-create` e `azure vm create` hanno alias che è possibile usare per accedere rapidamente alle distribuzioni più comuni e alle versioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-136">The `azure vm quick-create` and `azure vm create` commands have aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="3cb9c-137">Usare alias è in genere più veloce che specificare editore, offerta, SKU e versione ogni volta che si crea una VM:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-137">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="3cb9c-138">Alias</span><span class="sxs-lookup"><span data-stu-id="3cb9c-138">Alias</span></span> | <span data-ttu-id="3cb9c-139">Autore</span><span class="sxs-lookup"><span data-stu-id="3cb9c-139">Publisher</span></span> | <span data-ttu-id="3cb9c-140">Offerta</span><span class="sxs-lookup"><span data-stu-id="3cb9c-140">Offer</span></span> | <span data-ttu-id="3cb9c-141">SKU</span><span class="sxs-lookup"><span data-stu-id="3cb9c-141">SKU</span></span> | <span data-ttu-id="3cb9c-142">Versione</span><span class="sxs-lookup"><span data-stu-id="3cb9c-142">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="3cb9c-143">CentOS</span><span class="sxs-lookup"><span data-stu-id="3cb9c-143">CentOS</span></span> |<span data-ttu-id="3cb9c-144">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="3cb9c-144">OpenLogic</span></span> |<span data-ttu-id="3cb9c-145">Centos</span><span class="sxs-lookup"><span data-stu-id="3cb9c-145">Centos</span></span> |<span data-ttu-id="3cb9c-146">7,2</span><span class="sxs-lookup"><span data-stu-id="3cb9c-146">7.2</span></span> |<span data-ttu-id="3cb9c-147">più recenti</span><span class="sxs-lookup"><span data-stu-id="3cb9c-147">latest</span></span> |
| <span data-ttu-id="3cb9c-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="3cb9c-148">CoreOS</span></span> |<span data-ttu-id="3cb9c-149">CoreOS</span><span class="sxs-lookup"><span data-stu-id="3cb9c-149">CoreOS</span></span> |<span data-ttu-id="3cb9c-150">CoreOS</span><span class="sxs-lookup"><span data-stu-id="3cb9c-150">CoreOS</span></span> |<span data-ttu-id="3cb9c-151">Stabile</span><span class="sxs-lookup"><span data-stu-id="3cb9c-151">Stable</span></span> |<span data-ttu-id="3cb9c-152">più recenti</span><span class="sxs-lookup"><span data-stu-id="3cb9c-152">latest</span></span> |
| <span data-ttu-id="3cb9c-153">Debian</span><span class="sxs-lookup"><span data-stu-id="3cb9c-153">Debian</span></span> |<span data-ttu-id="3cb9c-154">credativ</span><span class="sxs-lookup"><span data-stu-id="3cb9c-154">credativ</span></span> |<span data-ttu-id="3cb9c-155">Debian</span><span class="sxs-lookup"><span data-stu-id="3cb9c-155">Debian</span></span> |<span data-ttu-id="3cb9c-156">8</span><span class="sxs-lookup"><span data-stu-id="3cb9c-156">8</span></span> |<span data-ttu-id="3cb9c-157">più recenti</span><span class="sxs-lookup"><span data-stu-id="3cb9c-157">latest</span></span> |
| <span data-ttu-id="3cb9c-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="3cb9c-158">openSUSE</span></span> |<span data-ttu-id="3cb9c-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="3cb9c-159">SUSE</span></span> |<span data-ttu-id="3cb9c-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="3cb9c-160">openSUSE</span></span> |<span data-ttu-id="3cb9c-161">13.2</span><span class="sxs-lookup"><span data-stu-id="3cb9c-161">13.2</span></span> |<span data-ttu-id="3cb9c-162">più recenti</span><span class="sxs-lookup"><span data-stu-id="3cb9c-162">latest</span></span> |
| <span data-ttu-id="3cb9c-163">RHEL</span><span class="sxs-lookup"><span data-stu-id="3cb9c-163">RHEL</span></span> |<span data-ttu-id="3cb9c-164">Redhat</span><span class="sxs-lookup"><span data-stu-id="3cb9c-164">Redhat</span></span> |<span data-ttu-id="3cb9c-165">RHEL</span><span class="sxs-lookup"><span data-stu-id="3cb9c-165">RHEL</span></span> |<span data-ttu-id="3cb9c-166">7,2</span><span class="sxs-lookup"><span data-stu-id="3cb9c-166">7.2</span></span> |<span data-ttu-id="3cb9c-167">più recenti</span><span class="sxs-lookup"><span data-stu-id="3cb9c-167">latest</span></span> |
| <span data-ttu-id="3cb9c-168">SLES</span><span class="sxs-lookup"><span data-stu-id="3cb9c-168">SLES</span></span> |<span data-ttu-id="3cb9c-169">SLES</span><span class="sxs-lookup"><span data-stu-id="3cb9c-169">SLES</span></span> |<span data-ttu-id="3cb9c-170">SLES</span><span class="sxs-lookup"><span data-stu-id="3cb9c-170">SLES</span></span> |<span data-ttu-id="3cb9c-171">12-SP1</span><span class="sxs-lookup"><span data-stu-id="3cb9c-171">12-SP1</span></span> |<span data-ttu-id="3cb9c-172">più recenti</span><span class="sxs-lookup"><span data-stu-id="3cb9c-172">latest</span></span> |
| <span data-ttu-id="3cb9c-173">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="3cb9c-173">UbuntuLTS</span></span> |<span data-ttu-id="3cb9c-174">Canonical</span><span class="sxs-lookup"><span data-stu-id="3cb9c-174">Canonical</span></span> |<span data-ttu-id="3cb9c-175">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="3cb9c-175">UbuntuServer</span></span> |<span data-ttu-id="3cb9c-176">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="3cb9c-176">14.04.4-LTS</span></span> |<span data-ttu-id="3cb9c-177">più recenti</span><span class="sxs-lookup"><span data-stu-id="3cb9c-177">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="3cb9c-178">Usare la propria immagine</span><span class="sxs-lookup"><span data-stu-id="3cb9c-178">Use your own image</span></span>
<span data-ttu-id="3cb9c-179">Per personalizzazioni specifiche è possibile usare un'immagine basata su una VM di Azure esistente *acquisendo* tale VM.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-179">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span></span> <span data-ttu-id="3cb9c-180">È anche possibile caricare un'immagine creata in locale.</span><span class="sxs-lookup"><span data-stu-id="3cb9c-180">You can also upload an image created on-premises.</span></span> <span data-ttu-id="3cb9c-181">Per altre informazioni sulle distribuzioni supportate e su come usare immagini personalizzate, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-181">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="3cb9c-182">Distribuzioni approvate per Azure</span><span class="sxs-lookup"><span data-stu-id="3cb9c-182">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="3cb9c-183">Informazioni per distribuzioni non approvate</span><span class="sxs-lookup"><span data-stu-id="3cb9c-183">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* [<span data-ttu-id="3cb9c-184">Caricare e creare una VM Linux da un'immagine disco personalizzata</span><span class="sxs-lookup"><span data-stu-id="3cb9c-184">Upload and create a Linux VM from custom disk image</span></span>](upload-vhd.md)
* <span data-ttu-id="3cb9c-185">[Come acquisire una macchina virtuale Linux come modello di Resource Manager](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="3cb9c-185">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md).</span></span>
  
  * <span data-ttu-id="3cb9c-186">Comandi di avvio rapido di esempio per l'acquisizione di una VM esistente:</span><span class="sxs-lookup"><span data-stu-id="3cb9c-186">Quick-start example commands to capture an existing VM:</span></span>
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a><span data-ttu-id="3cb9c-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3cb9c-187">Next steps</span></span>
* <span data-ttu-id="3cb9c-188">Creare una VM Linux dal [portale](quick-create-portal.md), con l'[interfaccia della riga di comando](quick-create-cli.md) oppure usando un [modello di Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3cb9c-188">Create a Linux VM from the [portal](quick-create-portal.md), with the [CLI](quick-create-cli.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="3cb9c-189">Dopo aver creato una VM Linux, [aggiungere un disco dati](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="3cb9c-189">After creating a Linux VM, [add a data disk](add-disk.md).</span></span>
* <span data-ttu-id="3cb9c-190">Azioni rapide per [reimpostare una password o chiavi SSH e gestire gli utenti](using-vmaccess-extension.md)</span><span class="sxs-lookup"><span data-stu-id="3cb9c-190">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md)</span></span>

