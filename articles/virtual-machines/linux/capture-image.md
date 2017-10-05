---
title: Acquisire un'immagine di una macchina virtuale Linux in Azure usando l'interfaccia della riga di comando 2.0 | Microsoft Docs
description: Acquisire un'immagine di una macchina virtuale di Azure da usare per le distribuzioni di massa tramite l'interfaccia della riga di comando di Azure 2.0.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 19b573f77f2ee84600955d00d30bdb16c84e3623
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="c6bc8-103">Come creare un'immagine di una macchina virtuale o un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="c6bc8-103">How to create an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of the tutorial-->

<span data-ttu-id="c6bc8-104">Per creare più copie di una macchina virtuale da usare in Azure, acquisire un'immagine della macchina virtuale o il disco rigido virtuale del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-104">To create multiple copies of a virtual machine (VM) to use in Azure, capture an image of the VM or the OS VHD.</span></span> <span data-ttu-id="c6bc8-105">Per creare un'immagine, è necessario rimuovere le informazioni sull'account personale, in modo da poter distribuire più volte in totale sicurezza.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-105">To create an image, you need remove personal account information which makes it safer to deploy multiple times.</span></span> <span data-ttu-id="c6bc8-106">Nei passaggi seguenti si eseguirà il deprovisioning di una macchina virtuale esistente e quindi la deallocazione e la creazione di un'immagine.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-106">In the following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="c6bc8-107">È possibile usare questa immagine per creare macchine virtuali in qualsiasi gruppo di risorse all'interno della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-107">You can use this image to create VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="c6bc8-108">Per creare una copia della macchina virtuale Linux esistente per il backup o il debug o per caricare un disco rigido virtuale Linux specializzato da una macchina virtuale locale, vedere [Caricare e creare una VM Linux da un'immagine disco personalizzata](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="c6bc8-108">If you want to create a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="c6bc8-109">È possibile anche usare **Packer** per creare una configurazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-109">You can also use **Packer** to create your custom configuration.</span></span> <span data-ttu-id="c6bc8-110">Per altre informazioni sull'uso di Packer, vedere [Come usare Packer per creare immagini di macchine virtuali di Linux in Azure](build-image-with-packer.md).</span><span class="sxs-lookup"><span data-stu-id="c6bc8-110">For more information on using Packer, see [How to use Packer to create Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="c6bc8-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="c6bc8-111">Before you begin</span></span>
<span data-ttu-id="c6bc8-112">Accertarsi che siano soddisfatti i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c6bc8-112">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="c6bc8-113">È necessario aver creato una macchina virtuale di Azure nel modello di distribuzione Resource Manager tramite l'utilizzo di dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-113">You need an Azure VM created in the Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="c6bc8-114">Se non è stata creata una macchina virtuale Linux, è possibile usare il [portale](quick-create-portal.md), l'[interfaccia della riga di comando di Azure](quick-create-cli.md) o i [modelli di Resource Manager](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="c6bc8-114">If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md), the [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="c6bc8-115">Configurare la macchina virtuale in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-115">Configure the VM as needed.</span></span> <span data-ttu-id="c6bc8-116">Ad esempio, [aggiungere dischi dati](add-disk.md), applicare aggiornamenti e installare applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="c6bc8-117">È necessario anche aver installato l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e aver eseguito l'accesso a un account Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c6bc8-117">You also need to have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="c6bc8-118">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="c6bc8-118">Quick commands</span></span>

<span data-ttu-id="c6bc8-119">Per una versione semplificata di questo argomento e per informazioni sulle procedure di testing e valutazione o sulle macchine virtuali in Azure, vedere [Creare un'immagine personalizzata di una macchina virtuale di Azure tramite l'interfaccia della riga di comando](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="c6bc8-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-the-vm"></a><span data-ttu-id="c6bc8-120">Passaggio 1: Eseguire il deprovisioning della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c6bc8-120">Step 1: Deprovision the VM</span></span>
<span data-ttu-id="c6bc8-121">Eseguire il deprovisioning della macchina virtuale usando l'agente della macchina virtuale di Azure per eliminare file e dati specifici della macchina.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-121">You deprovision the VM, using the Azure VM agent, to delete machine specific files and data.</span></span> <span data-ttu-id="c6bc8-122">Usare il comando `waagent` con il parametro *-deprovision+user* nella macchina virtuale Linux di origine.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-122">Use the `waagent` command with the *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="c6bc8-123">Per altre informazioni, vedere [Guida dell'utente dell'agente Linux di Azure](../windows/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c6bc8-123">For more information, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="c6bc8-124">Connettersi alla VM Linux tramite un client SSH.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-124">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="c6bc8-125">Nella finestra SSH digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c6bc8-125">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="c6bc8-126">Eseguire questo comando solo su una VM che si intende acquisire come immagine.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-126">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="c6bc8-127">Ciò non garantisce che dall'immagine vengano cancellate tutte le informazioni sensibili o che l'immagine sia adatta per la ridistribuzione.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-127">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="c6bc8-128">Il parametro *+user* rimuove anche l'ultimo account utente di cui è stato effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-128">The *+user* parameter also removes the last provisioned user account.</span></span> <span data-ttu-id="c6bc8-129">Se invece si vuole mantenere le credenziali dell'account nella macchina virtuale, usare semplicemente *-deprovision* per non rimuovere l'account utente.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-129">If you want to keep account credentials in the VM, just use *-deprovision* to leave the user account in place.</span></span>
 
3. <span data-ttu-id="c6bc8-130">Digitare **y** per continuare.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-130">Type **y** to continue.</span></span> <span data-ttu-id="c6bc8-131">È possibile aggiungere il parametro **-force** per evitare questo passaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-131">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="c6bc8-132">Dopo aver eseguito il comando, digitare **exit**.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-132">After the command completes, type **exit**.</span></span> <span data-ttu-id="c6bc8-133">Questo passaggio chiude il client SSH.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-133">This step closes the SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="c6bc8-134">Passaggio 2: Creare l'immagine della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c6bc8-134">Step 2: Create VM image</span></span>
<span data-ttu-id="c6bc8-135">Usare l'interfaccia della riga di comando di Azure 2.0 per contrassegnare la macchina virtuale come generalizzata e acquisire l'immagine.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-135">Use the Azure CLI 2.0 to mark the VM as generalized and capture the image.</span></span> <span data-ttu-id="c6bc8-136">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-136">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c6bc8-137">I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="c6bc8-138">Deallocare la macchina virtuale su cui è stato eseguito il deprovisioning con [az vm deallocate](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="c6bc8-138">Deallocate the VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="c6bc8-139">L'esempio seguente dealloca la VM denominata *myVM* nel gruppo di risorse *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c6bc8-139">The following example deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="c6bc8-140">Contrassegnare la macchina virtuale come generalizzata con il comando [az vm generalize](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="c6bc8-140">Mark the VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="c6bc8-141">Nell'esempio seguente la macchina virtuale denominata *myVM* viene contrassegnata come generalizzata nel gruppo di risorse *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c6bc8-141">The following example marks the the VM named *myVM* in the resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="c6bc8-142">Creare ora un'immagine della risorsa macchina virtuale con [az image create](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="c6bc8-142">Now create an image of the VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="c6bc8-143">Nell'esempio seguente viene creata un'immagine denominata *myImage* nel gruppo di risorse denominato *myResourceGroup* usando la risorsa della macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="c6bc8-143">The following example creates an image named *myImage* in the resource group named *myResourceGroup* using the VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="c6bc8-144">L'immagine viene creata nello stesso gruppo di risorse della macchina virtuale di origine.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-144">The image is created in the same resource group as your source VM.</span></span> <span data-ttu-id="c6bc8-145">Con questa immagine è possibile creare macchine virtuali in qualsiasi gruppo di risorse all'interno della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="c6bc8-146">Da una prospettiva di gestione, si consiglia di creare un gruppo di risorse specifico per le risorse e le immagini della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-146">From a management perspective, you may wish to create a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="c6bc8-147">Passaggio 3: Distribuire una VM dall'immagine acquisita</span><span class="sxs-lookup"><span data-stu-id="c6bc8-147">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="c6bc8-148">Creare una macchina virtuale usando l'immagine creata con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c6bc8-148">Create a VM using the image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c6bc8-149">Nell'esempio seguente viene creata una macchina virtuale denominata *myVMDeployed* dall'immagine denominata *myImage*:</span><span class="sxs-lookup"><span data-stu-id="c6bc8-149">The following example creates a VM named *myVMDeployed* from the image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-the-vm-in-another-resource-group"></a><span data-ttu-id="c6bc8-150">Creazione della macchina virtuale in un altro gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c6bc8-150">Creating the VM in another resource group</span></span> 

<span data-ttu-id="c6bc8-151">È possibile creare macchine virtuali da un'immagine in qualsiasi gruppo di risorse all'interno della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="c6bc8-152">Per creare una macchina virtuale in un gruppo di risorse diverso rispetto all'immagine, specificare l'ID di risorsa completa per l'immagine.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-152">To create a VM in a different resource group than the image, specify the full resource ID to your image.</span></span> <span data-ttu-id="c6bc8-153">Usare [az image list](/cli/azure/image#list) per visualizzare un elenco di immagini.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-153">Use [az image list](/cli/azure/image#list) to view a list of images.</span></span> <span data-ttu-id="c6bc8-154">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c6bc8-154">The output is similar to the following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="c6bc8-155">L'esempio seguente usa [az vm create](/cli/azure/vm#create) per creare una macchina virtuale in un gruppo di risorse diverso rispetto all'immagine di origine, specificando l'ID di risorsa immagine:</span><span class="sxs-lookup"><span data-stu-id="c6bc8-155">The following example uses [az vm create](/cli/azure/vm#create) to create a VM in a different resource group than the source image by specifying the image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-the-deployment"></a><span data-ttu-id="c6bc8-156">Passaggio 4: Verificare la distribuzione</span><span class="sxs-lookup"><span data-stu-id="c6bc8-156">Step 4: Verify the deployment</span></span>

<span data-ttu-id="c6bc8-157">Connettersi ora con SSH alla macchina virtuale creata per verificare la distribuzione e iniziare a usare la nuova VM.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-157">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="c6bc8-158">Per connettersi tramite SSH, trovare l'indirizzo IP o il nome di dominio completo della macchina virtuale con [az vm show](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="c6bc8-158">To connect via SSH, find the IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="c6bc8-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6bc8-159">Next steps</span></span>
<span data-ttu-id="c6bc8-160">È possibile creare più macchine virtuali da un'immagine di macchina virtuale di origine.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="c6bc8-161">Se è necessario apportare modifiche all'immagine:</span><span class="sxs-lookup"><span data-stu-id="c6bc8-161">If you need to make changes to your image:</span></span> 

- <span data-ttu-id="c6bc8-162">Creare una macchina virtuale da un'immagine dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-162">Create a VM from your image.</span></span>
- <span data-ttu-id="c6bc8-163">Apportare aggiornamenti o modifiche alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="c6bc8-164">Seguire nuovamente i passaggi per eseguire il deprovisioning, deallocare, generalizzare e creare un'immagine.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-164">Follow the steps again to deprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="c6bc8-165">Usare la nuova immagine per le distribuzioni future.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-165">Use this new image for future deployments.</span></span> <span data-ttu-id="c6bc8-166">Se si desidera, eliminare l'immagine originale.</span><span class="sxs-lookup"><span data-stu-id="c6bc8-166">If desired, delete the original image.</span></span>

<span data-ttu-id="c6bc8-167">Per altre informazioni sulla gestione delle macchine virtuali con l'interfaccia della riga di comando, vedere [Interfaccia della riga di comando di Azure 2.0](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c6bc8-167">For more information on managing your VMs with the CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
