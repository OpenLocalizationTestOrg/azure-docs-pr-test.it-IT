---
title: un'immagine di una VM Linux in Azure utilizzando CLI 2.0 aaaCapture | Documenti Microsoft
description: Acquisire un'immagine di toouse una macchina virtuale di Azure per distribuzioni di massa tramite hello CLI di Azure 2.0.
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
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="ed64a-103">Come toocreate un'immagine di una macchina virtuale o un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="ed64a-103">How toocreate an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of hello tutorial-->

<span data-ttu-id="ed64a-104">toocreate più copie di una macchina virtuale (VM) toouse in Azure, acquisire un'immagine di macchina virtuale hello o hello disco rigido virtuale del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ed64a-104">toocreate multiple copies of a virtual machine (VM) toouse in Azure, capture an image of hello VM or hello OS VHD.</span></span> <span data-ttu-id="ed64a-105">toocreate un'immagine, è necessario rimuovere le informazioni personali che rende più sicura toodeploy più volte.</span><span class="sxs-lookup"><span data-stu-id="ed64a-105">toocreate an image, you need remove personal account information which makes it safer toodeploy multiple times.</span></span> <span data-ttu-id="ed64a-106">In hello alla procedura seguente si deprovisioning di una macchina virtuale esistente, rilasciare e creare un'immagine.</span><span class="sxs-lookup"><span data-stu-id="ed64a-106">In hello following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="ed64a-107">È possibile utilizzare questa immagine toocreate macchine virtuali, in qualsiasi gruppo di risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ed64a-107">You can use this image toocreate VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="ed64a-108">Se si desidera toocreate una copia della VM Linux esistente per il backup o il debug o si carica un VHD Linux specializzato da una macchina virtuale locale, vedere [caricare e creare una VM Linux dall'immagine del disco personalizzato](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="ed64a-108">If you want toocreate a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="ed64a-109">È inoltre possibile utilizzare **chi** toocreate configurazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="ed64a-109">You can also use **Packer** toocreate your custom configuration.</span></span> <span data-ttu-id="ed64a-110">Per ulteriori informazioni sull'utilizzo di chi, vedere [come le immagini di macchina virtuale Linux di toouse chi toocreate in Azure](build-image-with-packer.md).</span><span class="sxs-lookup"><span data-stu-id="ed64a-110">For more information on using Packer, see [How toouse Packer toocreate Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="ed64a-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="ed64a-111">Before you begin</span></span>
<span data-ttu-id="ed64a-112">Verificare che siano soddisfatti hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="ed64a-112">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="ed64a-113">È necessario una macchina virtuale di Azure creata nel modello di distribuzione di gestione risorse hello utilizzando dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="ed64a-113">You need an Azure VM created in hello Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="ed64a-114">Se è stata creata una VM Linux, è possibile utilizzare hello [portale](quick-create-portal.md), hello [CLI di Azure](quick-create-cli.md), o [modelli di gestione risorse](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="ed64a-114">If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="ed64a-115">Configurare hello macchina virtuale in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="ed64a-115">Configure hello VM as needed.</span></span> <span data-ttu-id="ed64a-116">Ad esempio, [aggiungere dischi dati](add-disk.md), applicare aggiornamenti e installare applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ed64a-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="ed64a-117">È inoltre necessario hello toohave più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ed64a-117">You also need toohave hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="ed64a-118">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="ed64a-118">Quick commands</span></span>

<span data-ttu-id="ed64a-119">Per una versione semplificata di questo argomento, per il test, la valutazione o di formazione su macchine virtuali in Azure, vedere [creare un'immagine personalizzata di una macchina virtuale di Azure utilizzando hello CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="ed64a-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-hello-vm"></a><span data-ttu-id="ed64a-120">Passaggio 1: Eseguire il deprovisioning hello VM</span><span class="sxs-lookup"><span data-stu-id="ed64a-120">Step 1: Deprovision hello VM</span></span>
<span data-ttu-id="ed64a-121">Eseguire il deprovisioning hello macchina virtuale con l'agente VM di Azure hello, toodelete file specifici di computer e i dati.</span><span class="sxs-lookup"><span data-stu-id="ed64a-121">You deprovision hello VM, using hello Azure VM agent, toodelete machine specific files and data.</span></span> <span data-ttu-id="ed64a-122">Hello utilizzare `waagent` con hello *-deprovisioning + user* parametro nell'origine VM Linux.</span><span class="sxs-lookup"><span data-stu-id="ed64a-122">Use hello `waagent` command with hello *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="ed64a-123">Per ulteriori informazioni, vedere hello [Guida dell'utente dell'agente Linux di Azure](../windows/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="ed64a-123">For more information, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="ed64a-124">Connettersi tooyour VM Linux utilizzando un client SSH.</span><span class="sxs-lookup"><span data-stu-id="ed64a-124">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="ed64a-125">Nella finestra di hello SSH, digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ed64a-125">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="ed64a-126">Solo il seguente comando in una macchina virtuale che si desidera toocapture come immagine.</span><span class="sxs-lookup"><span data-stu-id="ed64a-126">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="ed64a-127">Non garantisce che l'immagine hello viene cancellato di tutte le informazioni riservate o adatto per la ridistribuzione.</span><span class="sxs-lookup"><span data-stu-id="ed64a-127">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="ed64a-128">Hello *+ user* parametro anche rimuove l'ultimo account di provisioning utente hello.</span><span class="sxs-lookup"><span data-stu-id="ed64a-128">hello *+user* parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="ed64a-129">Se si desidera tookeep le credenziali dell'account in hello macchina virtuale, usare semplicemente *-deprovisioning* tooleave hello account utente sul posto.</span><span class="sxs-lookup"><span data-stu-id="ed64a-129">If you want tookeep account credentials in hello VM, just use *-deprovision* tooleave hello user account in place.</span></span>
 
3. <span data-ttu-id="ed64a-130">Tipo **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="ed64a-130">Type **y** toocontinue.</span></span> <span data-ttu-id="ed64a-131">È possibile aggiungere hello **-force** tooavoid parametro questo passaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="ed64a-131">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="ed64a-132">Al termine del comando di hello, digitare **uscire**.</span><span class="sxs-lookup"><span data-stu-id="ed64a-132">After hello command completes, type **exit**.</span></span> <span data-ttu-id="ed64a-133">Questo passaggio consente di chiudere client SSH hello.</span><span class="sxs-lookup"><span data-stu-id="ed64a-133">This step closes hello SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="ed64a-134">Passaggio 2: Creare l'immagine della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ed64a-134">Step 2: Create VM image</span></span>
<span data-ttu-id="ed64a-135">Utilizzare hello toomark hello Azure CLI 2.0 VM come generalizzato e acquisire l'immagine hello.</span><span class="sxs-lookup"><span data-stu-id="ed64a-135">Use hello Azure CLI 2.0 toomark hello VM as generalized and capture hello image.</span></span> <span data-ttu-id="ed64a-136">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="ed64a-136">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ed64a-137">I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="ed64a-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="ed64a-138">Deallocare una macchina virtuale che deprovisioning con hello [az vm deallocare](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="ed64a-138">Deallocate hello VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="ed64a-139">esempio Hello dealloca hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ed64a-139">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="ed64a-140">Hello contrassegno VM come generalizzata con [generalizzare la macchina virtuale az](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="ed64a-140">Mark hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="ed64a-141">Hello in seguito esempio contrassegni hello hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup* come generalizzato:</span><span class="sxs-lookup"><span data-stu-id="ed64a-141">hello following example marks hello hello VM named *myVM* in hello resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="ed64a-142">Creare un'immagine di risorsa di macchina virtuale hello con [immagine az creare](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="ed64a-142">Now create an image of hello VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="ed64a-143">esempio Hello crea un'immagine denominata *myImage* nel gruppo di risorse hello denominato *myResourceGroup* utilizzando hello risorsa di macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="ed64a-143">hello following example creates an image named *myImage* in hello resource group named *myResourceGroup* using hello VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="ed64a-144">Hello immagine è creata in hello stesso gruppo di risorse come la macchina virtuale di origine.</span><span class="sxs-lookup"><span data-stu-id="ed64a-144">hello image is created in hello same resource group as your source VM.</span></span> <span data-ttu-id="ed64a-145">Con questa immagine è possibile creare macchine virtuali in qualsiasi gruppo di risorse all'interno della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ed64a-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="ed64a-146">Da una prospettiva di gestione, è preferibile toocreate un gruppo di risorse specifiche per le risorse macchina virtuale e le immagini.</span><span class="sxs-lookup"><span data-stu-id="ed64a-146">From a management perspective, you may wish toocreate a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="ed64a-147">Passaggio 3: Creare una macchina virtuale dall'immagine acquisita hello</span><span class="sxs-lookup"><span data-stu-id="ed64a-147">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="ed64a-148">Creare una macchina virtuale utilizzando l'immagine di hello è stato creato con [creare vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="ed64a-148">Create a VM using hello image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="ed64a-149">esempio Hello crea una macchina virtuale denominata *myVMDeployed* dall'immagine hello denominato *myImage*:</span><span class="sxs-lookup"><span data-stu-id="ed64a-149">hello following example creates a VM named *myVMDeployed* from hello image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a><span data-ttu-id="ed64a-150">Creazione di hello macchina virtuale in un altro gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="ed64a-150">Creating hello VM in another resource group</span></span> 

<span data-ttu-id="ed64a-151">È possibile creare macchine virtuali da un'immagine in qualsiasi gruppo di risorse all'interno della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ed64a-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="ed64a-152">toocreate una macchina virtuale in un gruppo di risorse diverso da quello immagine hello, specificare l'immagine di tooyour ID completo della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="ed64a-152">toocreate a VM in a different resource group than hello image, specify hello full resource ID tooyour image.</span></span> <span data-ttu-id="ed64a-153">Utilizzare [elenco immagini az](/cli/azure/image#list) tooview un elenco di immagini.</span><span class="sxs-lookup"><span data-stu-id="ed64a-153">Use [az image list](/cli/azure/image#list) tooview a list of images.</span></span> <span data-ttu-id="ed64a-154">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="ed64a-154">hello output is similar toohello following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="ed64a-155">Hello seguente utilizza [creare vm az](/cli/azure/vm#create) toocreate una macchina virtuale in un gruppo di risorse diverso da quello immagine di origine hello specificando l'ID di risorsa immagine hello:</span><span class="sxs-lookup"><span data-stu-id="ed64a-155">hello following example uses [az vm create](/cli/azure/vm#create) toocreate a VM in a different resource group than hello source image by specifying hello image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a><span data-ttu-id="ed64a-156">Passaggio 4: Verificare la distribuzione di hello</span><span class="sxs-lookup"><span data-stu-id="ed64a-156">Step 4: Verify hello deployment</span></span>

<span data-ttu-id="ed64a-157">Ora SSH toohello macchina virtuale è stato creato distribuzione hello tooverify e iniziare a usare hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed64a-157">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="ed64a-158">tooconnect tramite SSH, trovare hello o indirizzo IP della macchina virtuale con [Mostra vm az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="ed64a-158">tooconnect via SSH, find hello IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="ed64a-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed64a-159">Next steps</span></span>
<span data-ttu-id="ed64a-160">È possibile creare più macchine virtuali da un'immagine di macchina virtuale di origine.</span><span class="sxs-lookup"><span data-stu-id="ed64a-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="ed64a-161">Se è necessario l'immagine di tooyour toomake modifiche:</span><span class="sxs-lookup"><span data-stu-id="ed64a-161">If you need toomake changes tooyour image:</span></span> 

- <span data-ttu-id="ed64a-162">Creare una macchina virtuale da un'immagine dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ed64a-162">Create a VM from your image.</span></span>
- <span data-ttu-id="ed64a-163">Apportare aggiornamenti o modifiche alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="ed64a-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="ed64a-164">Seguire hello passaggi nuovamente toodeprovision, rilasciare, generalizzare e creare un'immagine.</span><span class="sxs-lookup"><span data-stu-id="ed64a-164">Follow hello steps again toodeprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="ed64a-165">Usare la nuova immagine per le distribuzioni future.</span><span class="sxs-lookup"><span data-stu-id="ed64a-165">Use this new image for future deployments.</span></span> <span data-ttu-id="ed64a-166">Se necessario, eliminare l'immagine originale hello.</span><span class="sxs-lookup"><span data-stu-id="ed64a-166">If desired, delete hello original image.</span></span>

<span data-ttu-id="ed64a-167">Per ulteriori informazioni sulla gestione delle macchine virtuali con hello CLI, vedere [CLI di Azure 2.0](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ed64a-167">For more information on managing your VMs with hello CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
