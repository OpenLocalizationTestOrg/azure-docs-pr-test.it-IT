---
title: immagini di macchina virtuale con hello CLI di Azure personalizzate aaaCreate | Documenti Microsoft
description: 'Esercitazione: creare un''immagine di macchina virtuale personalizzata utilizzando hello CLI di Azure.'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a><span data-ttu-id="9faa3-103">Creare un'immagine personalizzata di una macchina virtuale di Azure utilizzando hello CLI</span><span class="sxs-lookup"><span data-stu-id="9faa3-103">Create a custom image of an Azure VM using hello CLI</span></span>

<span data-ttu-id="9faa3-104">Le immagini personalizzate sono come le immagini di marketplace, ma si possono creare autonomamente.</span><span class="sxs-lookup"><span data-stu-id="9faa3-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="9faa3-105">Immagini personalizzate possono essere utilizzati toobootstrap configurazioni, ad esempio il precaricamento di applicazioni, configurazioni dell'applicazione e altre configurazioni del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="9faa3-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="9faa3-106">In questa esercitazione viene creata un'immagine personalizzata di una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9faa3-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="9faa3-107">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="9faa3-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9faa3-108">Eseguire il deprovisioning e generalizzare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="9faa3-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="9faa3-109">Creare un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="9faa3-109">Create a custom image</span></span>
> * <span data-ttu-id="9faa3-110">Creare una VM da un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="9faa3-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="9faa3-111">Elenco di tutte le immagini di hello nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="9faa3-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="9faa3-112">Eliminare un'immagine</span><span class="sxs-lookup"><span data-stu-id="9faa3-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9faa3-113">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="9faa3-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9faa3-114">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="9faa3-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9faa3-115">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9faa3-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="9faa3-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="9faa3-116">Before you begin</span></span>

<span data-ttu-id="9faa3-117">passaggi di Hello riportati di seguito in dettaglio come tootake una macchina virtuale esistente e attivare i dati in un oggetto personalizzato riutilizzabile immagine che si possono usare toocreate nuove istanze di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9faa3-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="9faa3-118">esempio di hello toocomplete in questa esercitazione, è necessario disporre di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="9faa3-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="9faa3-119">Se necessario, questo [script di esempio](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) può crearne una appositamente.</span><span class="sxs-lookup"><span data-stu-id="9faa3-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="9faa3-120">Quando il lavoro esercitazione hello, sostituire il gruppo di risorse di hello e VM nomi dove necessario.</span><span class="sxs-lookup"><span data-stu-id="9faa3-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="9faa3-121">Creare un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="9faa3-121">Create a custom image</span></span>

<span data-ttu-id="9faa3-122">toocreate un'immagine di una macchina virtuale, è necessario tooprepare hello VM deprovisioning, la deallocazione e quindi contrassegnando origine hello VM come generalizzato.</span><span class="sxs-lookup"><span data-stu-id="9faa3-122">toocreate an image of a virtual machine, you need tooprepare hello VM by deprovisioning, deallocating, and then marking hello source VM as generalized.</span></span> <span data-ttu-id="9faa3-123">Una volta hello che macchina virtuale è stata preparata, è possibile creare un'immagine.</span><span class="sxs-lookup"><span data-stu-id="9faa3-123">Once hello VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-hello-vm"></a><span data-ttu-id="9faa3-124">Eseguire il deprovisioning hello VM</span><span class="sxs-lookup"><span data-stu-id="9faa3-124">Deprovision hello VM</span></span> 

<span data-ttu-id="9faa3-125">Deprovisioning generalizza hello VM rimuovendo le informazioni specifiche del computer.</span><span class="sxs-lookup"><span data-stu-id="9faa3-125">Deprovisioning generalizes hello VM by removing machine-specific information.</span></span> <span data-ttu-id="9faa3-126">La generalizzazione rende possibili toodeploy più macchine virtuali da una singola immagine.</span><span class="sxs-lookup"><span data-stu-id="9faa3-126">This generalization makes it possible toodeploy many VMs from a single image.</span></span> <span data-ttu-id="9faa3-127">Durante il deprovisioning, nome host hello viene reimpostato troppo*localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="9faa3-127">During deprovisioning, hello host name is reset too*localhost.localdomain*.</span></span> <span data-ttu-id="9faa3-128">Vengono eliminati anche i lease DHCP memorizzati nella cache, le chiavi host SSH, le configurazioni nameserver e le password radicele.</span><span class="sxs-lookup"><span data-stu-id="9faa3-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="9faa3-129">hello toodeprovision macchina virtuale, utilizzare l'agente VM di Azure hello (waagent).</span><span class="sxs-lookup"><span data-stu-id="9faa3-129">toodeprovision hello VM, use hello Azure VM agent (waagent).</span></span> <span data-ttu-id="9faa3-130">agente VM di Azure Hello viene installato nella macchina virtuale hello e gestisce il provisioning e l'interazione con il Controller di infrastruttura di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9faa3-130">hello Azure VM agent is installed on hello VM and manages provisioning and interacting with hello Azure Fabric Controller.</span></span> <span data-ttu-id="9faa3-131">Per ulteriori informazioni, vedere hello [Guida dell'utente dell'agente Linux di Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="9faa3-131">For more information, see hello [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="9faa3-132">Tooyour macchina virtuale di connettersi tramite SSH e hello esecuzione comando toodeprovision Ciao macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9faa3-132">Connect tooyour VM using SSH and run hello command toodeprovision hello VM.</span></span> <span data-ttu-id="9faa3-133">Con hello `+user` argomento, l'ultimo account di provisioning utente hello ed eventuali dati associati vengono eliminati anche.</span><span class="sxs-lookup"><span data-stu-id="9faa3-133">With hello `+user` argument, hello last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="9faa3-134">Sostituire l'indirizzo IP di esempio hello con indirizzo IP pubblico hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9faa3-134">Replace hello example IP address with hello public IP address of your VM.</span></span>

<span data-ttu-id="9faa3-135">SSH toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9faa3-135">SSH toohello VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="9faa3-136">Eseguire il deprovisioning hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9faa3-136">Deprovision hello VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="9faa3-137">Chiudere una sessione SSH hello.</span><span class="sxs-lookup"><span data-stu-id="9faa3-137">Close hello SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="9faa3-138">Rilasciare e contrassegnare hello VM come generalizzato</span><span class="sxs-lookup"><span data-stu-id="9faa3-138">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="9faa3-139">toocreate un'immagine, hello VM deve toobe deallocato.</span><span class="sxs-lookup"><span data-stu-id="9faa3-139">toocreate an image, hello VM needs toobe deallocated.</span></span> <span data-ttu-id="9faa3-140">Deallocare hello VM utilizzando [az vm deallocare](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="9faa3-140">Deallocate hello VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="9faa3-141">Infine, impostare lo stato di hello di hello VM come generalizzata con [generalizzare la macchina virtuale az](/cli//azure/vm#generalize) affinché hello piattaforma Azure sappia hello VM sia stato generalizzato.</span><span class="sxs-lookup"><span data-stu-id="9faa3-141">Finally, set hello state of hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so hello Azure platform knows hello VM has been generalized.</span></span> <span data-ttu-id="9faa3-142">È possibile creare solo un'immagine da una VM generalizzata.</span><span class="sxs-lookup"><span data-stu-id="9faa3-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a><span data-ttu-id="9faa3-143">Creare l'immagine di hello</span><span class="sxs-lookup"><span data-stu-id="9faa3-143">Create hello image</span></span>

<span data-ttu-id="9faa3-144">Ora è possibile creare un'immagine di macchina virtuale hello utilizzando [immagine az creare](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="9faa3-144">Now you can create an image of hello VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="9faa3-145">esempio Hello crea un'immagine denominata *myImage* da una macchina virtuale denominata *myVM*.</span><span class="sxs-lookup"><span data-stu-id="9faa3-145">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="9faa3-146">Creare macchine virtuali da immagini hello</span><span class="sxs-lookup"><span data-stu-id="9faa3-146">Create VMs from hello image</span></span>

<span data-ttu-id="9faa3-147">Dopo aver creato un'immagine, è possibile creare nuove macchine virtuali da hello immagine utilizzando [creare vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="9faa3-147">Now that you have an image, you can create one or more new VMs from hello image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="9faa3-148">esempio Hello crea una macchina virtuale denominata *myVMfromImage* dall'immagine hello denominato *myImage*.</span><span class="sxs-lookup"><span data-stu-id="9faa3-148">hello following example creates a VM named *myVMfromImage* from hello image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="9faa3-149">Gestione delle immagini</span><span class="sxs-lookup"><span data-stu-id="9faa3-149">Image management</span></span> 

<span data-ttu-id="9faa3-150">Di seguito sono riportati alcuni esempi di attività comuni di gestione di immagini e come toocomplete loro utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="9faa3-150">Here are some examples of common image management tasks and how toocomplete them using hello Azure CLI.</span></span>

<span data-ttu-id="9faa3-151">Elencare tutte le immagini per nome in formato tabella.</span><span class="sxs-lookup"><span data-stu-id="9faa3-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="9faa3-152">Eliminare un'immagine.</span><span class="sxs-lookup"><span data-stu-id="9faa3-152">Delete an image.</span></span> <span data-ttu-id="9faa3-153">In questo esempio elimina hello immagine denominata *myOldImage* da hello *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="9faa3-153">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="9faa3-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9faa3-154">Next steps</span></span>

<span data-ttu-id="9faa3-155">In questa esercitazione è stata creata un'immagine di macchina virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="9faa3-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="9faa3-156">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="9faa3-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9faa3-157">Eseguire il deprovisioning e generalizzare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="9faa3-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="9faa3-158">Creare un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="9faa3-158">Create a custom image</span></span>
> * <span data-ttu-id="9faa3-159">Creare una VM da un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="9faa3-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="9faa3-160">Elenco di tutte le immagini di hello nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="9faa3-160">List all hello images in your subscription</span></span>
> * <span data-ttu-id="9faa3-161">Eliminare un'immagine</span><span class="sxs-lookup"><span data-stu-id="9faa3-161">Delete an image</span></span>

<span data-ttu-id="9faa3-162">Spostare toohello Avanti toolearn esercitazione sulle macchine virtuali a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="9faa3-162">Advance toohello next tutorial toolearn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="9faa3-163">[Creare macchine virtuali a disponibilità elevata](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="9faa3-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

