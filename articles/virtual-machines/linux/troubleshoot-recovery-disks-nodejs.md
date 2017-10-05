---
title: Uso di una VM per la risoluzione dei problemi delle macchine virtuali Linux tramite l'interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: Informazioni su come risolvere i problemi delle VM Linux connettendo il disco del sistema operativo a una VM di ripristino tramite l'interfaccia della riga di comando di Azure 1.0
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: d817358211f123c96d899c5cff88cc47aeb5c9c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-cli-10"></a><span data-ttu-id="4f8af-103">Risolvere i problemi relativi a una VM Linux collegando il disco del sistema operativo a una VM di ripristino tramite l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4f8af-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="4f8af-104">Se nella VM Linux viene rilevato un errore di avvio o del disco, potrebbe essere necessario eseguire dei passaggi per la risoluzione dei problemi sul disco rigido virtuale stesso.</span><span class="sxs-lookup"><span data-stu-id="4f8af-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="4f8af-105">Un esempio comune è una voce non valida in `/etc/fstab` che impedisce il corretto avvio della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f8af-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="4f8af-106">Questo articolo illustra come usare l'interfaccia della riga di comando di Azure 1.0 per connettere il disco rigido virtuale a un'altra VM Linux al fine di risolvere eventuali errori e quindi ricreare la VM originale.</span><span class="sxs-lookup"><span data-stu-id="4f8af-106">This article details how to use the Azure CLI 1.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="4f8af-107">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="4f8af-107">CLI versions to complete the task</span></span>
<span data-ttu-id="4f8af-108">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="4f8af-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="4f8af-109">[Interfaccia della riga di comando di Azure 1.0](#recovery-process-overview): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="4f8af-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="4f8af-110">[Interfaccia della riga di comando di Azure 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="4f8af-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="4f8af-111">Panoramica del processo di ripristino</span><span class="sxs-lookup"><span data-stu-id="4f8af-111">Recovery process overview</span></span>
<span data-ttu-id="4f8af-112">I passaggi per la risoluzione dei problemi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="4f8af-112">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="4f8af-113">Eliminare la macchina virtuale su cui si riscontrano i problemi, mantenendo i dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="4f8af-113">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="4f8af-114">Collegare e montare il disco rigido virtuale in un'altra VM Linux per risolvere i problemi riscontrati.</span><span class="sxs-lookup"><span data-stu-id="4f8af-114">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="4f8af-115">Connettersi alla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="4f8af-115">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="4f8af-116">Modificare i file o eseguire eventuali strumenti per risolvere i problemi nel disco rigido virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="4f8af-116">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="4f8af-117">Smontare e scollegare il disco rigido virtuale dalla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="4f8af-117">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="4f8af-118">Creare una VM usando il disco rigido virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="4f8af-118">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="4f8af-119">Controllare di aver installato la [versione più recente dell'interfaccia della riga di comando di Azure 1.0 ](../../cli-install-nodejs.md), di aver eseguito l'accesso e di usare la modalità Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="4f8af-119">Make sure that you have [the latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="4f8af-120">Negli esempi seguenti sostituire i nomi dei parametri con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="4f8af-120">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="4f8af-121">Alcuni esempi di nomi dei parametri sono `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="4f8af-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="4f8af-122">Individuare i problemi di avvio</span><span class="sxs-lookup"><span data-stu-id="4f8af-122">Determine boot issues</span></span>
<span data-ttu-id="4f8af-123">Esaminare l'output seriale per determinare perché la macchina virtuale non è in grado di avviarsi correttamente.</span><span class="sxs-lookup"><span data-stu-id="4f8af-123">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="4f8af-124">Un esempio comune è una voce non valida in `/etc/fstab`, oppure l'eliminazione o lo spostamento del disco rigido virtuale sottostante.</span><span class="sxs-lookup"><span data-stu-id="4f8af-124">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="4f8af-125">L'esempio seguente ottiene l'output seriale dalla macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4f8af-125">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4f8af-126">Esaminare l'output seriale per determinare perché la macchina virtuale non è in grado di avviarsi correttamente.</span><span class="sxs-lookup"><span data-stu-id="4f8af-126">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="4f8af-127">Se l'output seriale non fornisce alcuna indicazione, potrebbe essere necessario esaminare i file di log in `/var/log` dopo aver collegato il disco rigido virtuale a una macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="4f8af-127">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="4f8af-128">Visualizzare i dettagli del disco rigido virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="4f8af-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="4f8af-129">Prima di collegare il disco rigido virtuale a un'altra macchina virtuale, è necessario identificare il nome del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f8af-129">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="4f8af-130">L'esempio seguente ottiene le informazioni relative alla macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4f8af-130">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4f8af-131">Cercare il valore `Vhd URI` nell'output ottenuto con il comando precedente.</span><span class="sxs-lookup"><span data-stu-id="4f8af-131">Look for `Vhd URI` in the output from the preceding command.</span></span> <span data-ttu-id="4f8af-132">L'ultima riga dell'output di esempio seguente mostra il valore `Vhd URI`:</span><span class="sxs-lookup"><span data-stu-id="4f8af-132">The following truncated example output shows the `Vhd URI` on the last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myVM"
+ Looking up the NIC "myNic"
+ Looking up the public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a><span data-ttu-id="4f8af-133">Eliminare la VM esistente</span><span class="sxs-lookup"><span data-stu-id="4f8af-133">Delete existing VM</span></span>
<span data-ttu-id="4f8af-134">In Azure, i dischi rigidi virtuali e le macchine virtuali sono due risorse distinte.</span><span class="sxs-lookup"><span data-stu-id="4f8af-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="4f8af-135">In un disco rigido virtuale sono archiviati il sistema operativo, le applicazioni e le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="4f8af-135">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="4f8af-136">La macchina virtuale è invece costituita da metadati che definiscono le dimensioni o il percorso, e da risorse di riferimento, ad esempio un disco rigido virtuale o una scheda di interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f8af-136">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="4f8af-137">A ogni disco rigido virtuale associato a una macchina virtuale viene assegnato un lease.</span><span class="sxs-lookup"><span data-stu-id="4f8af-137">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="4f8af-138">È possibile collegare e scollegare i dischi dati anche quando la macchina virtuale è in esecuzione, mentre non è possibile scollegare il disco del sistema operativo, a meno che la risorsa di macchina non sia stata eliminata.</span><span class="sxs-lookup"><span data-stu-id="4f8af-138">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="4f8af-139">Il lease continua ad associare il disco del sistema operativo e la macchina virtuale anche quando questa viene arrestata e deallocata.</span><span class="sxs-lookup"><span data-stu-id="4f8af-139">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="4f8af-140">Il primo passaggio per ripristinare la macchina virtuale consiste nell'eliminare la risorsa della macchina virtuale stessa.</span><span class="sxs-lookup"><span data-stu-id="4f8af-140">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="4f8af-141">Anche se si elimina la macchina virtuale, i dischi rigidi virtuali restano nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4f8af-141">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="4f8af-142">Dopo aver eliminato la macchina virtuale, il disco rigido virtuale viene collegato a un'altra macchina virtuale per diagnosticare e risolvere gli errori.</span><span class="sxs-lookup"><span data-stu-id="4f8af-142">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="4f8af-143">L'esempio seguente elimina la macchina virtuale denominata `myVM` dal gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4f8af-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="4f8af-144">Attendere il completamento dell'eliminazione della macchina virtuale prima di collegare il disco rigido virtuale a un'altra macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f8af-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="4f8af-145">Il lease del disco rigido virtuale che lo associa alla macchina virtuale deve essere rilasciato prima di poter collegare il disco a un'altra macchina.</span><span class="sxs-lookup"><span data-stu-id="4f8af-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="4f8af-146">Collegare il disco rigido virtuale esistente a un'altra macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4f8af-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="4f8af-147">Nei passaggi successivi viene utilizzata un'altra macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="4f8af-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="4f8af-148">Il disco rigido virtuale esistente viene collegato alla macchina virtuale usata per la risoluzione dei problemi, grazie alla quale è possibile individuare e modificare il contenuto del disco.</span><span class="sxs-lookup"><span data-stu-id="4f8af-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="4f8af-149">Questo processo consente, ad esempio, di correggere eventuali errori di configurazione, di esaminare applicazioni aggiuntive o file del registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="4f8af-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="4f8af-150">Scegliere o creare un'altra macchina virtuale da usare per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="4f8af-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="4f8af-151">Quando si collega il disco rigido virtuale esistente, specificare l'URL del disco ottenuto con il comando `azure vm show` precedente.</span><span class="sxs-lookup"><span data-stu-id="4f8af-151">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `azure vm show` command.</span></span> <span data-ttu-id="4f8af-152">Nell'esempio seguente il disco rigido virtuale esistente viene collegato alla macchina virtuale usata per la risoluzione dei problemi denominata `myVMRecovery` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4f8af-152">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="4f8af-153">Montare il disco dati collegato</span><span class="sxs-lookup"><span data-stu-id="4f8af-153">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="4f8af-154">Gli esempi seguenti mostrano in dettaglio i passaggi necessari in una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="4f8af-154">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="4f8af-155">Se si usa una diversa distribuzione Linux, ad esempio Red Hat Enterprise Linux o SUSE, i percorsi dei file di log e i comandi `mount` potrebbero differire.</span><span class="sxs-lookup"><span data-stu-id="4f8af-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="4f8af-156">Consultare la documentazione relativa alla distribuzione specifica per le opportune modifiche ai comandi.</span><span class="sxs-lookup"><span data-stu-id="4f8af-156">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="4f8af-157">Eseguire SSH nella macchina virtuale di cui risolvere i problemi usando le credenziali appropriate.</span><span class="sxs-lookup"><span data-stu-id="4f8af-157">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="4f8af-158">Se questo disco è il primo disco dati collegato alla macchina virtuale usata per la risoluzione dei problemi, è probabilmente connesso a `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="4f8af-158">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="4f8af-159">Usare `dmseg` per visualizzare i dischi collegati:</span><span class="sxs-lookup"><span data-stu-id="4f8af-159">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="4f8af-160">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="4f8af-160">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="4f8af-161">Nell'esempio precedente, il disco del sistema operativo è in `/dev/sda` e il disco temporaneo fornito per ogni macchina virtuale è in `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="4f8af-161">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="4f8af-162">Se sono presenti più dischi dati, devono trovarsi in `/dev/sdd`, `/dev/sde`, e così via.</span><span class="sxs-lookup"><span data-stu-id="4f8af-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="4f8af-163">Creare una directory per montare il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="4f8af-163">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="4f8af-164">L'esempio seguente crea una directory denominata `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="4f8af-164">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="4f8af-165">Se sul disco rigido virtuale esistente sono presenti più partizioni, montare la partizione richiesta.</span><span class="sxs-lookup"><span data-stu-id="4f8af-165">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="4f8af-166">L'esempio seguente monta la prima partizione primaria in `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="4f8af-166">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="4f8af-167">Si consiglia di montare i dischi dati nelle macchine virtuali in Azure usando l'identificatore univoco universale (UUID) del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f8af-167">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="4f8af-168">Per questo scenario, non è necessario montare il disco rigido virtuale usando il relativo l'UUID.</span><span class="sxs-lookup"><span data-stu-id="4f8af-168">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="4f8af-169">Durante il normale utilizzo, invece, modificare `/etc/fstab` per montare i dischi rigidi virtuali usando il nome di dispositivo anziché l'UUID può impedire il corretto avvio della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f8af-169">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="4f8af-170">Risolvere i problemi del disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="4f8af-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="4f8af-171">Dopo aver montato il disco rigido virtuale eseguire tutte le operazioni di manutenzione e i passaggi necessari per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="4f8af-171">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="4f8af-172">Dopo avere risolto i problemi, continuare con la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="4f8af-172">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="4f8af-173">Smontare e scollegare il disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="4f8af-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="4f8af-174">Dopo aver risolto gli errori, smontare e scollegare il disco rigido virtuale esistente dalla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="4f8af-174">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="4f8af-175">Non è possibile usare il disco rigido virtuale con altre macchine virtuali finché non viene rilasciato il lease che collega il disco rigido virtuale alla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="4f8af-175">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="4f8af-176">Dalla sessione SSH nella macchina virtuale usata per la risoluzione dei problemi, smontare il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="4f8af-176">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="4f8af-177">Modificare innanzitutto la directory padre del punto di montaggio:</span><span class="sxs-lookup"><span data-stu-id="4f8af-177">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="4f8af-178">A questo punto smontare il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="4f8af-178">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="4f8af-179">Nell'esempio viene smontato il dispositivo in `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="4f8af-179">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="4f8af-180">Scollegare il disco rigido virtuale dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f8af-180">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="4f8af-181">Chiudere la sessione SSH nella macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="4f8af-181">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="4f8af-182">Nell'interfaccia della riga di comando di Azure, elencare innanzitutto i dischi dati collegati alla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="4f8af-182">In the Azure CLI, first list the attached data disks to your troubleshooting VM.</span></span> <span data-ttu-id="4f8af-183">L'esempio seguente elenca i dischi dati collegati alla macchina virtuale denominata `myVMRecovery`nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4f8af-183">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="4f8af-184">Annotare il valore `Lun` del disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="4f8af-184">Note the `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="4f8af-185">L'output del comando di esempio seguente mostra il disco virtuale esistente collegato a LUN 0:</span><span class="sxs-lookup"><span data-stu-id="4f8af-185">The following example command output shows the existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up the VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="4f8af-186">Scollegare il disco dati dalla macchina virtuale usando il valore `Lun` appropriato:</span><span class="sxs-lookup"><span data-stu-id="4f8af-186">Detach the data disk from your VM using the applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="4f8af-187">Creare una macchina virtuale dal disco rigido originale</span><span class="sxs-lookup"><span data-stu-id="4f8af-187">Create VM from original hard disk</span></span>
<span data-ttu-id="4f8af-188">Per creare una macchina virtuale dal disco rigido virtuale originale, usare [questo modello di Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="4f8af-188">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="4f8af-189">Il modello JSON effettivo è disponibile all'indirizzo seguente:</span><span class="sxs-lookup"><span data-stu-id="4f8af-189">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="4f8af-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="4f8af-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="4f8af-191">Il modello distribuisce una macchina virtuale in una rete virtuale esistente, usando l'URL del disco rigido virtuale del comando precedente.</span><span class="sxs-lookup"><span data-stu-id="4f8af-191">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="4f8af-192">L'esempio seguente distribuisce il modello nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4f8af-192">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="4f8af-193">Rispondere ai prompt del modello, ad esempio inserendo il nome della macchina virtuale (`myDeployedVM` nell'esempio seguente), il tipo di sistema operativo (`Linux`) e le dimensioni della macchina virtuale (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="4f8af-193">Answer the prompts for the template such as VM name (`myDeployedVM` the following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="4f8af-194">Il valore `osDiskVhdUri` è lo stesso usato in precedenza per collegare il disco rigido virtuale esistente alla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="4f8af-194">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span> <span data-ttu-id="4f8af-195">Un esempio dell'output del comando e dei prompt è il seguente:</span><span class="sxs-lookup"><span data-stu-id="4f8af-195">An example of the command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment to complete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="4f8af-196">Riabilitare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="4f8af-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="4f8af-197">Quando si crea la macchina virtuale dal disco rigido virtuale esistente, la diagnostica di avvio potrebbe non essere abilitata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4f8af-197">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="4f8af-198">L'esempio seguente abilita l'estensione di diagnostica nella macchina virtuale denominata `myDeployedVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4f8af-198">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="4f8af-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4f8af-199">Next steps</span></span>
<span data-ttu-id="4f8af-200">Se si sono verificati problemi durante la connessione alla macchina virtuale, vedere l'articolo sulla [risoluzione dei problemi di connessione SSH a una macchina virtuale di Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4f8af-200">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4f8af-201">Per problemi relativi all'accesso alle applicazioni in esecuzione nella macchina virtuale, vedere [Risolvere i problemi di connettività delle applicazioni in una macchina virtuale di Azure per Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4f8af-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>