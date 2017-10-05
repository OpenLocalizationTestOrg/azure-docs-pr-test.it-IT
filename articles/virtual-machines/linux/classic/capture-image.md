---
title: Acquisire un'immagine di una macchina virtuale Linux | Microsoft Docs
description: Informazioni su come acquisire un'immagine di una macchina virtuale di Azure basata su Linux creata con il modello di distribuzione classica.
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
ms.openlocfilehash: ecde5dd3211bfbb290e6910d7d55136d079c6cf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-capture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="dd90b-103">Come acquisire una macchina virtuale Linux classica come immagine</span><span class="sxs-lookup"><span data-stu-id="dd90b-103">How to capture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dd90b-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="dd90b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="dd90b-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="dd90b-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="dd90b-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="dd90b-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="dd90b-107">Informazioni su come [eseguire questa procedura con il modello di Resource Manager](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd90b-107">Learn how to [perform these steps using the Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="dd90b-108">Questo articolo illustra come acquisire una macchina virtuale di Azure classica che esegue Linux come un'immagine per creare altre macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="dd90b-108">This article shows you how to capture a classic Azure virtual machine (VM) running Linux as an image to create other virtual machines.</span></span> <span data-ttu-id="dd90b-109">Tale immagine include il disco del sistema operativo e i dischi dati collegati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dd90b-109">This image includes the OS disk and data disks attached to the VM.</span></span> <span data-ttu-id="dd90b-110">Poiché la configurazione di rete non è inclusa, è necessario definirla quando si crea l'altra macchina virtuale dall'immagine.</span><span class="sxs-lookup"><span data-stu-id="dd90b-110">It doesn't include networking configuration, so you need to configure that when you create the other VM from the image.</span></span>

<span data-ttu-id="dd90b-111">Azure archivia l'immagine in **Immagini**, insieme a tutte le immagini caricate.</span><span class="sxs-lookup"><span data-stu-id="dd90b-111">Azure stores the image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="dd90b-112">Per altre informazioni sulle immagini, vedere [Informazioni sulle immagini di macchine virtuali in Azure][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="dd90b-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dd90b-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="dd90b-113">Before you begin</span></span>
<span data-ttu-id="dd90b-114">Questa procedura presuppone che sia stata creata una macchina virtuale di Azure tramite il modello di distribuzione classica e che sia stato configurato il sistema operativo, inclusi gli eventuali dischi dati connessi.</span><span class="sxs-lookup"><span data-stu-id="dd90b-114">These steps assume that you've already created an Azure VM using the Classic deployment model and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="dd90b-115">Se è necessario creare una macchina virtuale, leggere l'articolo [Come creare una macchina virtuale Linux][How to Create a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="dd90b-115">If you need to create a VM, read [How to Create a Linux Virtual Machine][How to Create a Linux Virtual Machine].</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="dd90b-116">Acquisizione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="dd90b-116">Capture the virtual machine</span></span>
1. <span data-ttu-id="dd90b-117">[Connettersi alla macchina virtuale](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) usando un client SSH di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="dd90b-117">[Connect to the VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="dd90b-118">Nella finestra di SSH digitare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="dd90b-118">In the SSH window, type the following command.</span></span> <span data-ttu-id="dd90b-119">L'output di `waagent` può variare leggermente, in base alla versione dell'utilità:</span><span class="sxs-lookup"><span data-stu-id="dd90b-119">The output from `waagent` may vary slightly depending on the version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="dd90b-120">Il comando precedente prova a pulire il sistema per renderlo idoneo per un nuovo provisioning.</span><span class="sxs-lookup"><span data-stu-id="dd90b-120">The preceding command attempts to clean the system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="dd90b-121">Questa operazione esegue le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd90b-121">This operation performs the following tasks:</span></span>

   * <span data-ttu-id="dd90b-122">Rimuove le chiavi host SSH (se Provisioning.RegenerateSshHostKeyPair è 'y' nel file di configurazione)</span><span class="sxs-lookup"><span data-stu-id="dd90b-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="dd90b-123">Cancella la configurazione NameServer in /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="dd90b-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="dd90b-124">Rimuove la password `root` dell'utente da /etc/shadow (se Provisioning.DeleteRootPassword è 'y' nel file di configurazione)</span><span class="sxs-lookup"><span data-stu-id="dd90b-124">Removes the `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="dd90b-125">Rimuove i lease client DHCP memorizzati nella cache</span><span class="sxs-lookup"><span data-stu-id="dd90b-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="dd90b-126">Ripristina il nome host su localhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="dd90b-126">Resets host name to localhost.localdomain</span></span>
   * <span data-ttu-id="dd90b-127">Elimina anche l'ultimo account utente (ottenuto da /var/lib/waagent) di cui è stato effettuato il provisioning **e i dati associati**.</span><span class="sxs-lookup"><span data-stu-id="dd90b-127">Deletes the last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="dd90b-128">Il deprovisioning elimina file e dati per "generalizzare" l'immagine.</span><span class="sxs-lookup"><span data-stu-id="dd90b-128">Deprovisioning deletes files and data to "generalize" the image.</span></span> <span data-ttu-id="dd90b-129">Eseguire questo comando solo su una macchina virtuale da acquisire come nuovo modello di immagine.</span><span class="sxs-lookup"><span data-stu-id="dd90b-129">Only run this command on a VM that you intend to capture as a new image template.</span></span> <span data-ttu-id="dd90b-130">Ciò non garantisce che dall'immagine vengano cancellate tutte le informazioni sensibili o che l'immagine sia adatta per la ridistribuzione a terze parti.</span><span class="sxs-lookup"><span data-stu-id="dd90b-130">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution to third parties.</span></span>

3. <span data-ttu-id="dd90b-131">Digitare **y** per continuare.</span><span class="sxs-lookup"><span data-stu-id="dd90b-131">Type **y** to continue.</span></span> <span data-ttu-id="dd90b-132">È possibile aggiungere il parametro `-force` per evitare questo passaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="dd90b-132">You can add the `-force` parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="dd90b-133">Digitare **Exit** per chiudere il client SSH.</span><span class="sxs-lookup"><span data-stu-id="dd90b-133">Type **Exit** to close the SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dd90b-134">I restanti passaggi presuppongono che l' [interfaccia della riga di comando di Azure](../../../cli-install-nodejs.md) sia stata già installata sul computer client.</span><span class="sxs-lookup"><span data-stu-id="dd90b-134">The remaining steps assume you have already [installed the Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="dd90b-135">Tutti i passaggi seguenti possono essere eseguiti anche nel [Portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dd90b-135">All the following steps can also be done in the [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="dd90b-136">Dal computer client, aprire l'interfaccia della riga di comando di Azure ed eseguire l'accesso alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd90b-136">From your client computer, open Azure CLI and login to your Azure subscription.</span></span> <span data-ttu-id="dd90b-137">Per informazioni dettagliate, leggere [Connettersi a una sottoscrizione Azure dall'interfaccia della riga di comando di Azure](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="dd90b-137">For details, read [Connect to an Azure subscription from the Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="dd90b-138">Accedere al Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd90b-138">In the Azure portal, log in to the portal.</span></span>

6. <span data-ttu-id="dd90b-139">Assicurarsi che sia attiva la modalità Gestione dei servizi:</span><span class="sxs-lookup"><span data-stu-id="dd90b-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="dd90b-140">Arrestare la macchina virtuale già sottoposta a deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="dd90b-140">Shut down the VM that is already deprovisioned.</span></span> <span data-ttu-id="dd90b-141">Nell'esempio seguente viene arrestata la macchina virtuale denominata `myVM`:</span><span class="sxs-lookup"><span data-stu-id="dd90b-141">The following example shuts down the VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="dd90b-142">Se necessario, è possibile visualizzare un elenco di tutte le macchine virtuali create nella propria sottoscrizione tramite il comando `azure vm list`</span><span class="sxs-lookup"><span data-stu-id="dd90b-142">If needed, you can view a list all the VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="dd90b-143">Se si usa il Portale di Azure, selezionare la macchina virtuale e fare clic su **Arresta** per arrestarla.</span><span class="sxs-lookup"><span data-stu-id="dd90b-143">If you're using the Azure portal, select the VM and click **Stop** to shut down the VM.</span></span>

8. <span data-ttu-id="dd90b-144">Quando la macchina virtuale viene arrestata, acquisire l'immagine.</span><span class="sxs-lookup"><span data-stu-id="dd90b-144">When the VM is stopped, capture the image.</span></span> <span data-ttu-id="dd90b-145">Nell'esempio seguente viene acquisita la macchina virtuale denominata `myVM` e viene creata un'immagine generalizzata denominata `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="dd90b-145">The following example captures the VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="dd90b-146">Il sottocomando `-t` consente di eliminare la macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="dd90b-146">The `-t` subcommand deletes the original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dd90b-147">Nel Portale di Azure è possibile acquisire un'immagine selezionando **Immagine** dal menu Hub.</span><span class="sxs-lookup"><span data-stu-id="dd90b-147">In the Azure portal, you can capture an image by selecting **Image** from the hub menu.</span></span> <span data-ttu-id="dd90b-148">Per l'immagine è necessario specificare le informazioni seguenti: nome, gruppo di risorse, posizione, tipo di sistema operativo e percorso BLOB di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="dd90b-148">You need to supply the following information for the image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="dd90b-149">La nuova immagine è ora disponibile nell'elenco di immagini che possono essere usate per configurare nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="dd90b-149">The new image is now available in the list of images that can be used to configure any new VM.</span></span> <span data-ttu-id="dd90b-150">È possibile visualizzarla con il comando:</span><span class="sxs-lookup"><span data-stu-id="dd90b-150">You can view it with the command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="dd90b-151">Nel [portale di Azure](http://portal.azure.com) la nuova immagine viene visualizzata in **Immagini VM (classico)** che appartiene a **Servizi di calcolo**.</span><span class="sxs-lookup"><span data-stu-id="dd90b-151">On the [Azure portal](http://portal.azure.com), the new image appears in the **VM images (classic)** that belongs to the **Compute** services.</span></span> <span data-ttu-id="dd90b-152">Per accedere a **Immagini VM (classico)**, fare clic su _Altri servizi_ nella parte inferiore dell'elenco di servizi di Azure e quindi eseguire una ricerca in **Servizi di calcolo**.</span><span class="sxs-lookup"><span data-stu-id="dd90b-152">You can access **VM images (classic)** by clicking _More services_ at the bottom of the Azure service list, and then looking in the **Compute** services.</span></span>   

   ![Acquisizione dell'immagine eseguita correttamente](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="dd90b-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd90b-154">Next steps</span></span>
<span data-ttu-id="dd90b-155">L'immagine può ora essere usata per creare macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="dd90b-155">The image is ready to be used to create VMs.</span></span> <span data-ttu-id="dd90b-156">È possibile usare il comando `azure vm create` dell'interfaccia della riga di comando di Azure e indicare il nome dell'immagine creata.</span><span class="sxs-lookup"><span data-stu-id="dd90b-156">You can use the Azure CLI command `azure vm create` and supply the image name you created.</span></span> <span data-ttu-id="dd90b-157">Per altre informazioni, vedere [Uso dell'interfaccia della riga di comando di Azure con il modello di distribuzione classica](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="dd90b-157">For more information, see [Using the Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="dd90b-158">In alternativa, usare il [Portale di Azure](http://portal.azure.com) per creare una macchina virtuale personalizzata tramite il metodo **Image** e selezionando l'immagine creata.</span><span class="sxs-lookup"><span data-stu-id="dd90b-158">Alternatively, use the [Azure portal](http://portal.azure.com) to create a custom VM by using the **Image** method and selecting the image you created.</span></span> <span data-ttu-id="dd90b-159">Per altre informazioni, vedere [Come creare una macchina virtuale personalizzata][How to Create a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="dd90b-159">For more information, see [How to Create a Custom VM][How to Create a Custom Virtual Machine].</span></span>

<span data-ttu-id="dd90b-160">**Vedere anche:** [Manuale dell'utente dell'agente Linux di Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="dd90b-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How to Create a Custom Virtual Machine]:create-custom.md
[How to Attach a Data Disk to a Virtual Machine]:attach-disk.md
[How to Create a Linux Virtual Machine]:create-custom.md
