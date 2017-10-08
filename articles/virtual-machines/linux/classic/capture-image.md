---
title: aaaCapture un'immagine di una VM Linux | Documenti Microsoft
description: Informazioni su come toocapture creata un'immagine di una basata su Linux Azure macchina virtuale (VM) con il modello di distribuzione classica hello.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="0ab61-103">Come toocapture una macchina virtuale di Linux classica come un'immagine</span><span class="sxs-lookup"><span data-stu-id="0ab61-103">How toocapture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0ab61-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0ab61-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0ab61-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="0ab61-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0ab61-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="0ab61-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0ab61-107">Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0ab61-107">Learn how too[perform these steps using hello Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0ab61-108">In questo articolo illustra come toocapture una classica macchina virtuale di Azure (VM) che eseguono Linux come un'immagine toocreate altre macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0ab61-108">This article shows you how toocapture a classic Azure virtual machine (VM) running Linux as an image toocreate other virtual machines.</span></span> <span data-ttu-id="0ab61-109">Questa immagine include disco del sistema operativo hello e dischi dati collegati toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0ab61-109">This image includes hello OS disk and data disks attached toohello VM.</span></span> <span data-ttu-id="0ab61-110">Configurazione di rete, non include pertanto è necessario tooconfigure che quando si crea hello altra macchina virtuale dall'immagine hello.</span><span class="sxs-lookup"><span data-stu-id="0ab61-110">It doesn't include networking configuration, so you need tooconfigure that when you create hello other VM from hello image.</span></span>

<span data-ttu-id="0ab61-111">Archivi Azure hello immagine in **immagini**, insieme a tutte le immagini caricate dall'utente.</span><span class="sxs-lookup"><span data-stu-id="0ab61-111">Azure stores hello image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="0ab61-112">Per altre informazioni sulle immagini, vedere [Informazioni sulle immagini di macchine virtuali in Azure][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="0ab61-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0ab61-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="0ab61-113">Before you begin</span></span>
<span data-ttu-id="0ab61-114">Questa procedura presuppone di aver già creato una macchina virtuale di Azure con modello di distribuzione classica hello e del sistema operativo configurato hello, incluso il collegamento a eventuali dischi dati.</span><span class="sxs-lookup"><span data-stu-id="0ab61-114">These steps assume that you've already created an Azure VM using hello Classic deployment model and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="0ab61-115">Se è necessario toocreate una macchina virtuale, leggere [come una macchina virtuale Linux tooCreate][How tooCreate a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="0ab61-115">If you need toocreate a VM, read [How tooCreate a Linux Virtual Machine][How tooCreate a Linux Virtual Machine].</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="0ab61-116">Acquisire una macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="0ab61-116">Capture hello virtual machine</span></span>
1. <span data-ttu-id="0ab61-117">[Connettersi toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) utilizzando un client SSH di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="0ab61-117">[Connect toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="0ab61-118">Nella finestra hello SSH, digitare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="0ab61-118">In hello SSH window, type hello following command.</span></span> <span data-ttu-id="0ab61-119">l'output di Hello `waagent` possono variare leggermente a seconda della versione di hello di questa utilità:</span><span class="sxs-lookup"><span data-stu-id="0ab61-119">hello output from `waagent` may vary slightly depending on hello version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="0ab61-120">Hello precedente comando tenta di sistema hello tooclean e rendono adatto per la riconfigurazione.</span><span class="sxs-lookup"><span data-stu-id="0ab61-120">hello preceding command attempts tooclean hello system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="0ab61-121">Questa operazione esegue hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="0ab61-121">This operation performs hello following tasks:</span></span>

   * <span data-ttu-id="0ab61-122">Rimuove le chiavi SSH host (se Provisioning.RegenerateSshHostKeyPair 'y' nel file di configurazione hello)</span><span class="sxs-lookup"><span data-stu-id="0ab61-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="0ab61-123">Cancella la configurazione NameServer in /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="0ab61-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="0ab61-124">Rimuove hello `root` password utente di ecc/shadow (se Provisioning.DeleteRootPassword 'y' nel file di configurazione hello)</span><span class="sxs-lookup"><span data-stu-id="0ab61-124">Removes hello `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="0ab61-125">Rimuove i lease client DHCP memorizzati nella cache</span><span class="sxs-lookup"><span data-stu-id="0ab61-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="0ab61-126">Reimposta host toolocalhost.localdomain nome</span><span class="sxs-lookup"><span data-stu-id="0ab61-126">Resets host name toolocalhost.localdomain</span></span>
   * <span data-ttu-id="0ab61-127">Elimina account provisioning utente ultimo hello (ottenuto dal /var/lib/waagent) **e i dati associati**.</span><span class="sxs-lookup"><span data-stu-id="0ab61-127">Deletes hello last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="0ab61-128">Deprovisioning Elimina i file e dati troppo "generalizzare" hello immagine.</span><span class="sxs-lookup"><span data-stu-id="0ab61-128">Deprovisioning deletes files and data too"generalize" hello image.</span></span> <span data-ttu-id="0ab61-129">Solo il seguente comando in una macchina virtuale che si desidera toocapture come nuovo modello di immagine.</span><span class="sxs-lookup"><span data-stu-id="0ab61-129">Only run this command on a VM that you intend toocapture as a new image template.</span></span> <span data-ttu-id="0ab61-130">Non garantisce che l'immagine hello viene cancellato di tutte le informazioni riservate o adatto per le parti toothird di ridistribuzione.</span><span class="sxs-lookup"><span data-stu-id="0ab61-130">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution toothird parties.</span></span>

3. <span data-ttu-id="0ab61-131">Tipo **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="0ab61-131">Type **y** toocontinue.</span></span> <span data-ttu-id="0ab61-132">È possibile aggiungere hello `-force` tooavoid parametro questo passaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="0ab61-132">You can add hello `-force` parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="0ab61-133">Tipo **uscita** client di tooclose hello SSH.</span><span class="sxs-lookup"><span data-stu-id="0ab61-133">Type **Exit** tooclose hello SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0ab61-134">Hello rimanenti passaggi si presuppone che si dispone già di [installato hello Azure CLI](../../../cli-install-nodejs.md) nel computer client.</span><span class="sxs-lookup"><span data-stu-id="0ab61-134">hello remaining steps assume you have already [installed hello Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="0ab61-135">Hello tutti i passaggi può essere eseguite anche in hello [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ab61-135">All hello following steps can also be done in hello [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="0ab61-136">Dal computer client, aprire Azure CLI e account di accesso tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0ab61-136">From your client computer, open Azure CLI and login tooyour Azure subscription.</span></span> <span data-ttu-id="0ab61-137">Per informazioni dettagliate, leggere [connettersi tooan sottoscrizione di Azure da hello Azure CLI](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="0ab61-137">For details, read [Connect tooan Azure subscription from hello Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="0ab61-138">Nel portale di Azure hello, accedi toohello portale.</span><span class="sxs-lookup"><span data-stu-id="0ab61-138">In hello Azure portal, log in toohello portal.</span></span>

6. <span data-ttu-id="0ab61-139">Assicurarsi che sia attiva la modalità Gestione dei servizi:</span><span class="sxs-lookup"><span data-stu-id="0ab61-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="0ab61-140">Arrestare hello macchina virtuale che è già sottoposta a deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="0ab61-140">Shut down hello VM that is already deprovisioned.</span></span> <span data-ttu-id="0ab61-141">Hello seguente arresta macchina virtuale denominata hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="0ab61-141">hello following example shuts down hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="0ab61-142">Se necessario, è possibile visualizzare un elenco di hello tutte le macchine virtuali creato nella sottoscrizione mediante`azure vm list`</span><span class="sxs-lookup"><span data-stu-id="0ab61-142">If needed, you can view a list all hello VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="0ab61-143">Se si usa hello portale di Azure, selezionare hello macchina virtuale e fare clic su **arrestare** arrestare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0ab61-143">If you're using hello Azure portal, select hello VM and click **Stop** to shut down hello VM.</span></span>

8. <span data-ttu-id="0ab61-144">Quando viene arrestato hello VM, acquisire l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="0ab61-144">When hello VM is stopped, capture hello image.</span></span> <span data-ttu-id="0ab61-145">Hello dopo le acquisizioni di esempio hello macchina virtuale denominata `myVM` e crea un'immagine generalizzata denominata `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="0ab61-145">hello following example captures hello VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="0ab61-146">Hello `-t` sottocomando eliminazioni hello macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="0ab61-146">hello `-t` subcommand deletes hello original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0ab61-147">Nel portale di Azure hello, è possibile acquisire un'immagine selezionando **immagine** dal menu di hub hello.</span><span class="sxs-lookup"><span data-stu-id="0ab61-147">In hello Azure portal, you can capture an image by selecting **Image** from hello hub menu.</span></span> <span data-ttu-id="0ab61-148">È necessario hello toosupply le seguenti informazioni per l'immagine di hello: nome gruppo di risorse, posizione, tipo di sistema operativo e percorso di archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="0ab61-148">You need toosupply hello following information for hello image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="0ab61-149">Hello nuova immagine è ora disponibile nell'elenco di hello delle immagini che possono essere tooconfigure di utilizzare qualsiasi nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0ab61-149">hello new image is now available in hello list of images that can be used tooconfigure any new VM.</span></span> <span data-ttu-id="0ab61-150">È possibile visualizzarli con il comando hello:</span><span class="sxs-lookup"><span data-stu-id="0ab61-150">You can view it with hello command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="0ab61-151">In hello [portale di Azure](http://portal.azure.com), hello nuova immagine viene visualizzata in hello **immagini di macchina virtuale (classico)** appartenente toohello **calcolo** servizi.</span><span class="sxs-lookup"><span data-stu-id="0ab61-151">On hello [Azure portal](http://portal.azure.com), hello new image appears in hello **VM images (classic)** that belongs toohello **Compute** services.</span></span> <span data-ttu-id="0ab61-152">È possibile accedere a **immagini di macchina virtuale (classico)** facendo _più servizi_ nella parte inferiore di hello di hello Azure service elenco e quindi cercare nella hello **calcolo** servizi.</span><span class="sxs-lookup"><span data-stu-id="0ab61-152">You can access **VM images (classic)** by clicking _More services_ at hello bottom of hello Azure service list, and then looking in hello **Compute** services.</span></span>   

   ![Acquisizione dell'immagine eseguita correttamente](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="0ab61-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0ab61-154">Next steps</span></span>
<span data-ttu-id="0ab61-155">immagine di Hello è pronto toobe utilizzato toocreate macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0ab61-155">hello image is ready toobe used toocreate VMs.</span></span> <span data-ttu-id="0ab61-156">È possibile utilizzare il comando di Azure CLI hello `azure vm create` e specificare il nome dell'immagine hello creato.</span><span class="sxs-lookup"><span data-stu-id="0ab61-156">You can use hello Azure CLI command `azure vm create` and supply hello image name you created.</span></span> <span data-ttu-id="0ab61-157">Per ulteriori informazioni, vedere [Using hello CLI di Azure con il modello di distribuzione classica](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="0ab61-157">For more information, see [Using hello Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="0ab61-158">In alternativa, utilizzare hello [portale di Azure](http://portal.azure.com) toocreate una macchina virtuale personalizzata tramite hello **immagine** (metodo) e selezionando hello immagine creata.</span><span class="sxs-lookup"><span data-stu-id="0ab61-158">Alternatively, use hello [Azure portal](http://portal.azure.com) toocreate a custom VM by using hello **Image** method and selecting hello image you created.</span></span> <span data-ttu-id="0ab61-159">Per ulteriori informazioni, vedere [come una macchina virtuale personalizzata tooCreate][How tooCreate a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="0ab61-159">For more information, see [How tooCreate a Custom VM][How tooCreate a Custom Virtual Machine].</span></span>

<span data-ttu-id="0ab61-160">**Vedere anche:** [Manuale dell'utente dell'agente Linux di Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0ab61-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
