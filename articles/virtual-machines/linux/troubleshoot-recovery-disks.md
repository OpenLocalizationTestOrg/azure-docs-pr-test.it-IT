---
title: Usare una macchina virtuale per la risoluzione dei problemi relativi a Linux con l'interfaccia della riga di comando di Azure 2.0 | Documentazione Microsoft
description: Informazioni su come risolvere i problemi delle macchine virtuali Linux connettendo il disco del sistema operativo a una macchina virtuale di ripristino tramite l'interfaccia della riga di comando di Azure 2.0
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 7a28accce1bd328b2b486b588c44d91b03e42122
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-with-the-azure-cli-20"></a><span data-ttu-id="afa0e-103">Risolvere i problemi relativi a una VM Linux collegando il disco del sistema operativo a una VM di ripristino tramite l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="afa0e-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM with the Azure CLI 2.0</span></span>
<span data-ttu-id="afa0e-104">Se nella VM Linux viene rilevato un errore di avvio o del disco, potrebbe essere necessario eseguire dei passaggi per la risoluzione dei problemi sul disco rigido virtuale stesso.</span><span class="sxs-lookup"><span data-stu-id="afa0e-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="afa0e-105">Un esempio comune è una voce non valida in `/etc/fstab` che impedisce il corretto avvio della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="afa0e-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="afa0e-106">Questo articolo illustra come usare l'interfaccia della riga di comando di Azure 2.0 per connettere il disco rigido virtuale a un'altra VM Linux al fine di risolvere eventuali errori e quindi ricreare la VM originale.</span><span class="sxs-lookup"><span data-stu-id="afa0e-106">This article details how to use the Azure CLI 2.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span> <span data-ttu-id="afa0e-107">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afa0e-107">You can also perform these steps with the [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="afa0e-108">Panoramica del processo di ripristino</span><span class="sxs-lookup"><span data-stu-id="afa0e-108">Recovery process overview</span></span>
<span data-ttu-id="afa0e-109">I passaggi per la risoluzione dei problemi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="afa0e-109">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="afa0e-110">Eliminare la macchina virtuale su cui si riscontrano i problemi, mantenendo i dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="afa0e-110">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="afa0e-111">Collegare e montare il disco rigido virtuale in un'altra VM Linux per risolvere i problemi riscontrati.</span><span class="sxs-lookup"><span data-stu-id="afa0e-111">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="afa0e-112">Connettersi alla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="afa0e-112">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="afa0e-113">Modificare i file o eseguire eventuali strumenti per risolvere i problemi nel disco rigido virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="afa0e-113">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="afa0e-114">Smontare e scollegare il disco rigido virtuale dalla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="afa0e-114">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="afa0e-115">Creare una VM usando il disco rigido virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="afa0e-115">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="afa0e-116">Per eseguire questi passaggi per la risoluzione dei problemi, è necessario aver installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e aver eseguito l'accesso a un account Azure con il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="afa0e-116">To perform these troubleshooting steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="afa0e-117">Negli esempi seguenti sostituire i nomi dei parametri con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="afa0e-117">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="afa0e-118">Alcuni esempi di nomi dei parametri sono `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="afa0e-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="afa0e-119">Individuare i problemi di avvio</span><span class="sxs-lookup"><span data-stu-id="afa0e-119">Determine boot issues</span></span>
<span data-ttu-id="afa0e-120">Esaminare l'output seriale per determinare perché la macchina virtuale non è in grado di avviarsi correttamente.</span><span class="sxs-lookup"><span data-stu-id="afa0e-120">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="afa0e-121">Un esempio comune è una voce non valida in `/etc/fstab`, oppure l'eliminazione o lo spostamento del disco rigido virtuale sottostante.</span><span class="sxs-lookup"><span data-stu-id="afa0e-121">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="afa0e-122">Ottenere i log di avvio con il comando [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="afa0e-122">Get the boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="afa0e-123">L'esempio seguente ottiene l'output seriale dalla macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="afa0e-123">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="afa0e-124">Esaminare l'output seriale per determinare perché la macchina virtuale non è in grado di avviarsi correttamente.</span><span class="sxs-lookup"><span data-stu-id="afa0e-124">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="afa0e-125">Se l'output seriale non fornisce alcuna indicazione, potrebbe essere necessario esaminare i file di log in `/var/log` dopo aver collegato il disco rigido virtuale a una macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="afa0e-125">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="afa0e-126">Visualizzare i dettagli del disco rigido virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="afa0e-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="afa0e-127">Prima di collegare il disco rigido virtuale (VHD) a un'altra macchina virtuale, è necessario identificare l'URI del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="afa0e-127">Before you can attach your virtual hard disk (VHD) to another VM, you need to identify the URI of the OS disk.</span></span> 

<span data-ttu-id="afa0e-128">Visualizzare le informazioni sulla macchina virtuale con il comando [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="afa0e-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="afa0e-129">Usare il flag `--query` per estrarre l'URI nel disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="afa0e-129">Use the `--query` flag to extract the URI to the OS disk.</span></span> <span data-ttu-id="afa0e-130">Nell'esempio seguente si ottengono le informazioni sul disco per la macchina virtuale denominata `myVM` nel gruppo di risorse denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="afa0e-130">The following example gets disk information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="afa0e-131">L'URI è analogo a **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="afa0e-131">The URI is similar to **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="afa0e-132">Eliminare la VM esistente</span><span class="sxs-lookup"><span data-stu-id="afa0e-132">Delete existing VM</span></span>
<span data-ttu-id="afa0e-133">In Azure, i dischi rigidi virtuali e le macchine virtuali sono due risorse distinte.</span><span class="sxs-lookup"><span data-stu-id="afa0e-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="afa0e-134">In un disco rigido virtuale sono archiviati il sistema operativo, le applicazioni e le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="afa0e-134">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="afa0e-135">La macchina virtuale è invece costituita da metadati che definiscono le dimensioni o il percorso, e da risorse di riferimento, ad esempio un disco rigido virtuale o una scheda di interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="afa0e-135">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="afa0e-136">A ogni disco rigido virtuale associato a una macchina virtuale viene assegnato un lease.</span><span class="sxs-lookup"><span data-stu-id="afa0e-136">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="afa0e-137">È possibile collegare e scollegare i dischi dati anche quando la macchina virtuale è in esecuzione, mentre non è possibile scollegare il disco del sistema operativo, a meno che la risorsa di macchina non sia stata eliminata.</span><span class="sxs-lookup"><span data-stu-id="afa0e-137">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="afa0e-138">Il lease continua ad associare il disco del sistema operativo e la macchina virtuale anche quando questa viene arrestata e deallocata.</span><span class="sxs-lookup"><span data-stu-id="afa0e-138">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="afa0e-139">Il primo passaggio per ripristinare la macchina virtuale consiste nell'eliminare la risorsa della macchina virtuale stessa.</span><span class="sxs-lookup"><span data-stu-id="afa0e-139">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="afa0e-140">Anche se si elimina la macchina virtuale, i dischi rigidi virtuali restano nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="afa0e-140">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="afa0e-141">Dopo aver eliminato la macchina virtuale, il disco rigido virtuale viene collegato a un'altra macchina virtuale per diagnosticare e risolvere gli errori.</span><span class="sxs-lookup"><span data-stu-id="afa0e-141">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="afa0e-142">Eliminare la macchina virtuale con il comando [az vm delete](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="afa0e-142">Delete the VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="afa0e-143">L'esempio seguente elimina la macchina virtuale denominata `myVM` dal gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="afa0e-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="afa0e-144">Attendere il completamento dell'eliminazione della macchina virtuale prima di collegare il disco rigido virtuale a un'altra macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="afa0e-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="afa0e-145">Il lease del disco rigido virtuale che lo associa alla macchina virtuale deve essere rilasciato prima di poter collegare il disco a un'altra macchina.</span><span class="sxs-lookup"><span data-stu-id="afa0e-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="afa0e-146">Collegare il disco rigido virtuale esistente a un'altra macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="afa0e-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="afa0e-147">Nei passaggi successivi viene utilizzata un'altra macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="afa0e-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="afa0e-148">Il disco rigido virtuale esistente viene collegato alla macchina virtuale usata per la risoluzione dei problemi, grazie alla quale è possibile individuare e modificare il contenuto del disco.</span><span class="sxs-lookup"><span data-stu-id="afa0e-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="afa0e-149">Questo processo consente, ad esempio, di correggere eventuali errori di configurazione, di esaminare applicazioni aggiuntive o file del registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="afa0e-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="afa0e-150">Scegliere o creare un'altra macchina virtuale da usare per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="afa0e-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="afa0e-151">Collegare il disco rigido virtuale con il comando [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="afa0e-151">Attach the existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="afa0e-152">Quando si collega il disco rigido virtuale esistente, specificare l'URI del disco ottenuto con il comando `az vm show` precedente.</span><span class="sxs-lookup"><span data-stu-id="afa0e-152">When you attach the existing virtual hard disk, specify the URI to the disk obtained in the preceding `az vm show` command.</span></span> <span data-ttu-id="afa0e-153">Nell'esempio seguente il disco rigido virtuale esistente viene collegato alla macchina virtuale usata per la risoluzione dei problemi denominata `myVMRecovery` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="afa0e-153">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="afa0e-154">Montare il disco dati collegato</span><span class="sxs-lookup"><span data-stu-id="afa0e-154">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="afa0e-155">Gli esempi seguenti mostrano in dettaglio i passaggi necessari in una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="afa0e-155">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="afa0e-156">Se si usa una diversa distribuzione Linux, ad esempio Red Hat Enterprise Linux o SUSE, i percorsi dei file di log e i comandi `mount` potrebbero differire.</span><span class="sxs-lookup"><span data-stu-id="afa0e-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="afa0e-157">Consultare la documentazione relativa alla distribuzione specifica per le opportune modifiche ai comandi.</span><span class="sxs-lookup"><span data-stu-id="afa0e-157">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="afa0e-158">Eseguire SSH nella macchina virtuale di cui risolvere i problemi usando le credenziali appropriate.</span><span class="sxs-lookup"><span data-stu-id="afa0e-158">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="afa0e-159">Se questo disco è il primo disco dati collegato alla macchina virtuale usata per la risoluzione dei problemi, è probabilmente connesso a `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="afa0e-159">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="afa0e-160">Usare `dmseg` per visualizzare i dischi collegati:</span><span class="sxs-lookup"><span data-stu-id="afa0e-160">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="afa0e-161">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="afa0e-161">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="afa0e-162">Nell'esempio precedente, il disco del sistema operativo è in `/dev/sda` e il disco temporaneo fornito per ogni macchina virtuale è in `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="afa0e-162">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="afa0e-163">Se sono presenti più dischi dati, devono trovarsi in `/dev/sdd`, `/dev/sde`, e così via.</span><span class="sxs-lookup"><span data-stu-id="afa0e-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="afa0e-164">Creare una directory per montare il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="afa0e-164">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="afa0e-165">L'esempio seguente crea una directory denominata `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="afa0e-165">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="afa0e-166">Se sul disco rigido virtuale esistente sono presenti più partizioni, montare la partizione richiesta.</span><span class="sxs-lookup"><span data-stu-id="afa0e-166">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="afa0e-167">L'esempio seguente monta la prima partizione primaria in `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="afa0e-167">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="afa0e-168">Si consiglia di montare i dischi dati nelle macchine virtuali in Azure usando l'identificatore univoco universale (UUID) del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="afa0e-168">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="afa0e-169">Per questo scenario, non è necessario montare il disco rigido virtuale usando il relativo l'UUID.</span><span class="sxs-lookup"><span data-stu-id="afa0e-169">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="afa0e-170">Durante il normale utilizzo, invece, modificare `/etc/fstab` per montare i dischi rigidi virtuali usando il nome di dispositivo anziché l'UUID può impedire il corretto avvio della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="afa0e-170">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="afa0e-171">Risolvere i problemi del disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="afa0e-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="afa0e-172">Dopo aver montato il disco rigido virtuale eseguire tutte le operazioni di manutenzione e i passaggi necessari per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="afa0e-172">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="afa0e-173">Dopo avere risolto i problemi, continuare con la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="afa0e-173">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="afa0e-174">Smontare e scollegare il disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="afa0e-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="afa0e-175">Dopo aver risolto gli errori, smontare e scollegare il disco rigido virtuale esistente dalla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="afa0e-175">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="afa0e-176">Non è possibile usare il disco rigido virtuale con altre macchine virtuali finché non viene rilasciato il lease che collega il disco rigido virtuale alla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="afa0e-176">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="afa0e-177">Dalla sessione SSH nella macchina virtuale usata per la risoluzione dei problemi, smontare il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="afa0e-177">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="afa0e-178">Modificare innanzitutto la directory padre del punto di montaggio:</span><span class="sxs-lookup"><span data-stu-id="afa0e-178">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="afa0e-179">A questo punto smontare il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="afa0e-179">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="afa0e-180">Nell'esempio viene smontato il dispositivo in `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="afa0e-180">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="afa0e-181">Scollegare il disco rigido virtuale dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="afa0e-181">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="afa0e-182">Chiudere la sessione SSH nella macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="afa0e-182">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="afa0e-183">Elencare i dischi dati collegati alla macchina virtuale per la risoluzione dei problemi con il comando [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="afa0e-183">List the attached data disks to your troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="afa0e-184">L'esempio seguente elenca i dischi dati collegati alla macchina virtuale denominata `myVMRecovery`nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="afa0e-184">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="afa0e-185">Annotare il valore del disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="afa0e-185">Note the name for your existing virtual hard disk.</span></span> <span data-ttu-id="afa0e-186">Il nome di un disco con l'URI **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** è, ad esempio, **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="afa0e-186">For example, the name of a disk with the URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="afa0e-187">Scollegare il disco dati dalla macchina virtuale con il comando [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="afa0e-187">Detach the data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="afa0e-188">Nell'esempio seguente il disco denominato `myVHD` viene scollegato dalla macchina virtuale denominata `myVMRecovery` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="afa0e-188">The following example detaches the disk named `myVHD` from the VM named `myVMRecovery` in the `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="afa0e-189">Creare una macchina virtuale dal disco rigido originale</span><span class="sxs-lookup"><span data-stu-id="afa0e-189">Create VM from original hard disk</span></span>
<span data-ttu-id="afa0e-190">Per creare una macchina virtuale dal disco rigido virtuale originale, usare [questo modello di Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="afa0e-190">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="afa0e-191">Il modello JSON effettivo è disponibile all'indirizzo seguente:</span><span class="sxs-lookup"><span data-stu-id="afa0e-191">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="afa0e-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="afa0e-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="afa0e-193">Il modello distribuisce una macchina virtuale usando l'URI del disco rigido virtuale dal comando precedente.</span><span class="sxs-lookup"><span data-stu-id="afa0e-193">The template deploys a VM using the VHD URI from the earlier command.</span></span> <span data-ttu-id="afa0e-194">Distribuire il modello con il comando [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="afa0e-194">Deploy the template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="afa0e-195">Specificare l'URI per il disco rigido virtuale originale e quindi specificare il tipo di sistema operativo e le dimensioni e il nome della macchina virtuale nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="afa0e-195">Provide the URI to your original VHD and then specify the OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="afa0e-196">Riabilitare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="afa0e-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="afa0e-197">Quando si crea la macchina virtuale dal disco rigido virtuale esistente, la diagnostica di avvio potrebbe non essere abilitata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="afa0e-197">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="afa0e-198">Abilitare la diagnostica di avvio con il comando [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="afa0e-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="afa0e-199">L'esempio seguente abilita l'estensione di diagnostica nella macchina virtuale denominata `myDeployedVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="afa0e-199">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="afa0e-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="afa0e-200">Next steps</span></span>
<span data-ttu-id="afa0e-201">Se si sono verificati problemi durante la connessione alla macchina virtuale, vedere l'articolo sulla [risoluzione dei problemi di connessione SSH a una macchina virtuale di Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afa0e-201">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="afa0e-202">Per problemi relativi all'accesso alle applicazioni in esecuzione nella macchina virtuale, vedere [Risolvere i problemi di connettività delle applicazioni in una macchina virtuale di Azure per Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afa0e-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>