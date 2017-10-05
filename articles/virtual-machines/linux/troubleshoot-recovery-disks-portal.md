---
title: Uso di una macchina virtuale Linux per la risoluzione dei problemi nel portale di Azure | Documentazione Microsoft
description: Informazioni su come risolvere i problemi delle macchine virtuali Linux connettendo il disco del sistema operativo a una macchina virtuale di ripristino nel portale di Azure
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
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: c96ff625c3e83f6fc9057f1163c877e8e0aed5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-portal"></a><span data-ttu-id="f35fb-103">Risolvere i problemi relativi a una macchina virtuale Linux collegando il disco del sistema operativo a una macchina virtuale di ripristino nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f35fb-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure portal</span></span>
<span data-ttu-id="f35fb-104">Se nella VM Linux viene rilevato un errore di avvio o del disco, potrebbe essere necessario eseguire dei passaggi per la risoluzione dei problemi sul disco rigido virtuale stesso.</span><span class="sxs-lookup"><span data-stu-id="f35fb-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="f35fb-105">Un esempio comune è una voce non valida in `/etc/fstab` che impedisce il corretto avvio della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="f35fb-106">Questo articolo illustra come usare il portale di Azure per connettere il disco rigido virtuale a un'altra VM Linux per risolvere eventuali errori e quindi ricreare la VM originale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-106">This article details how to use the Azure portal to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="f35fb-107">Panoramica del processo di ripristino</span><span class="sxs-lookup"><span data-stu-id="f35fb-107">Recovery process overview</span></span>
<span data-ttu-id="f35fb-108">I passaggi per la risoluzione dei problemi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="f35fb-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="f35fb-109">Eliminare la macchina virtuale su cui si riscontrano i problemi, mantenendo i dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="f35fb-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="f35fb-110">Collegare e montare il disco rigido virtuale in un'altra VM Linux per risolvere i problemi riscontrati.</span><span class="sxs-lookup"><span data-stu-id="f35fb-110">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="f35fb-111">Connettersi alla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="f35fb-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="f35fb-112">Modificare i file o eseguire eventuali strumenti per risolvere i problemi nel disco rigido virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="f35fb-113">Smontare e scollegare il disco rigido virtuale dalla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="f35fb-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="f35fb-114">Creare una VM usando il disco rigido virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-114">Create a VM using the original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="f35fb-115">Individuare i problemi di avvio</span><span class="sxs-lookup"><span data-stu-id="f35fb-115">Determine boot issues</span></span>
<span data-ttu-id="f35fb-116">Esaminare la diagnostica di avvio e la schermata della VM per determinare perché la macchina virtuale non è in grado di avviarsi correttamente.</span><span class="sxs-lookup"><span data-stu-id="f35fb-116">Examine the boot diagnostics and VM screenshot to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="f35fb-117">Un esempio comune è una voce non valida in `/etc/fstab`, oppure l'eliminazione o lo spostamento di un disco rigido virtuale sottostante.</span><span class="sxs-lookup"><span data-stu-id="f35fb-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="f35fb-118">Nel portale, selezionare la macchina virtuale e quindi scorrere verso il basso fino alla sezione **Supporto e risoluzione dei problemi**.</span><span class="sxs-lookup"><span data-stu-id="f35fb-118">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="f35fb-119">Fare clic su **Diagnostica di avvio** per i visualizzare i messaggi della console originati dalla VM.</span><span class="sxs-lookup"><span data-stu-id="f35fb-119">Click **Boot diagnostics** to view the console messages streamed from your VM.</span></span> <span data-ttu-id="f35fb-120">Esaminare i registri della console per cercare di determinare la causa del problema riscontrato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-120">Review the console logs to see if you can determine why the VM is encountering an issue.</span></span> <span data-ttu-id="f35fb-121">L'esempio seguente mostra una macchina virtuale bloccata in modalità di manutenzione che richiede l'intervento manuale:</span><span class="sxs-lookup"><span data-stu-id="f35fb-121">The following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Visualizzazione dei registri della console nella diagnostica di avvio della macchina virtuale](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="f35fb-123">È anche possibile fare clic su **Schermata** nella parte superiore del log della diagnostica di avvio per scaricare una schermata della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-123">You can also click **Screenshot** across the top of the boot diagnostics log to download a capture of the VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="f35fb-124">Visualizzare i dettagli del disco rigido virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="f35fb-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="f35fb-125">Prima di collegare il disco rigido virtuale a un'altra macchina virtuale, è necessario identificare il nome del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="f35fb-126">Selezionare il gruppo di risorse dal portale, quindi selezionare il proprio account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f35fb-126">Select your resource group from the portal, then select your storage account.</span></span> <span data-ttu-id="f35fb-127">Fare clic su **BLOB**, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f35fb-127">Click **Blobs**, as in the following example:</span></span>

![Selezionare il BLOB di archiviazione](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="f35fb-129">In genere è presente un contenitore denominato **vhds** che contiene i dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="f35fb-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="f35fb-130">Selezionare il contenitore per visualizzare un elenco dei dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="f35fb-130">Select the container to view a list of virtual hard disks.</span></span> <span data-ttu-id="f35fb-131">Annotare il nome del disco rigido virtuale desiderato. Il prefisso è in genere il nome della propria macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="f35fb-131">Note the name of your VHD (the prefix is usually the name of your VM):</span></span>

![Identificare il disco rigido virtuale nel contenitore di archiviazione](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="f35fb-133">Selezionare il disco rigido virtuale esistente dall'elenco e copiare l'URL, che verrà usato nei passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f35fb-133">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span></span>

![Copiare l'URL del disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="f35fb-135">Eliminare la VM esistente</span><span class="sxs-lookup"><span data-stu-id="f35fb-135">Delete existing VM</span></span>
<span data-ttu-id="f35fb-136">In Azure, i dischi rigidi virtuali e le macchine virtuali sono due risorse distinte.</span><span class="sxs-lookup"><span data-stu-id="f35fb-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="f35fb-137">In un disco rigido virtuale sono archiviati il sistema operativo, le applicazioni e le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="f35fb-137">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="f35fb-138">La macchina virtuale è invece costituita da metadati che definiscono le dimensioni o il percorso, e da risorse di riferimento, ad esempio un disco rigido virtuale o una scheda di interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-138">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="f35fb-139">A ogni disco rigido virtuale associato a una macchina virtuale viene assegnato un lease.</span><span class="sxs-lookup"><span data-stu-id="f35fb-139">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="f35fb-140">È possibile collegare e scollegare i dischi dati anche quando la macchina virtuale è in esecuzione, mentre non è possibile scollegare il disco del sistema operativo, a meno che la risorsa di macchina non sia stata eliminata.</span><span class="sxs-lookup"><span data-stu-id="f35fb-140">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="f35fb-141">Il lease continua ad associare il disco del sistema operativo e la macchina virtuale anche quando questa viene arrestata e deallocata.</span><span class="sxs-lookup"><span data-stu-id="f35fb-141">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="f35fb-142">Il primo passaggio per ripristinare la macchina virtuale consiste nell'eliminare la risorsa della macchina virtuale stessa.</span><span class="sxs-lookup"><span data-stu-id="f35fb-142">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="f35fb-143">Anche se si elimina la macchina virtuale, i dischi rigidi virtuali restano nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f35fb-143">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="f35fb-144">Dopo aver eliminato la macchina virtuale, il disco rigido virtuale viene collegato a un'altra macchina virtuale per diagnosticare e risolvere gli errori.</span><span class="sxs-lookup"><span data-stu-id="f35fb-144">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="f35fb-145">Selezionare la macchina virtuale nel portale, quindi fare clic su **Elimina**:</span><span class="sxs-lookup"><span data-stu-id="f35fb-145">Select your VM in the portal, then click **Delete**:</span></span>

![Schermata di diagnostica di avvio della macchina virtuale che mostra un errore di avvio](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="f35fb-147">Attendere il completamento dell'eliminazione della macchina virtuale prima di collegare il disco rigido virtuale a un'altra macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-147">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="f35fb-148">Il lease del disco rigido virtuale che lo associa alla macchina virtuale deve essere rilasciato prima di poter collegare il disco a un'altra macchina.</span><span class="sxs-lookup"><span data-stu-id="f35fb-148">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="f35fb-149">Collegare il disco rigido virtuale esistente a un'altra macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f35fb-149">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="f35fb-150">Nei passaggi successivi viene utilizzata un'altra macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="f35fb-150">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="f35fb-151">Il disco rigido virtuale esistente viene collegato alla macchina virtuale usata per la risoluzione dei problemi, grazie alla quale è possibile individuare e modificare il contenuto del disco.</span><span class="sxs-lookup"><span data-stu-id="f35fb-151">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span></span> <span data-ttu-id="f35fb-152">Questo processo consente, ad esempio, di correggere eventuali errori di configurazione, di esaminare applicazioni aggiuntive o file del registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="f35fb-152">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="f35fb-153">Scegliere o creare un'altra macchina virtuale da usare per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="f35fb-153">Choose or create another VM to use for troubleshooting purposes.</span></span>

1. <span data-ttu-id="f35fb-154">Nel portale, selezionare il gruppo di risorse e quindi la macchina virtuale da usare per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="f35fb-154">Select your resource group from the portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="f35fb-155">Selezionare **Dischi** e quindi fare clic su **Collega esistente**:</span><span class="sxs-lookup"><span data-stu-id="f35fb-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Collegare un disco esistente nel portale](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="f35fb-157">Per selezionare il disco rigido virtuale esistente, fare clic su **File VHD**:</span><span class="sxs-lookup"><span data-stu-id="f35fb-157">To select your existing virtual hard disk, click **VHD File**:</span></span>

    ![Cercare il disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="f35fb-159">Selezionare l'account e il contenitore di archiviazione, quindi fare clic sul disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="f35fb-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="f35fb-160">Fare clic sul pulsante **Seleziona** per confermare la scelta:</span><span class="sxs-lookup"><span data-stu-id="f35fb-160">Click the **Select** button to confirm your choice:</span></span>

    ![Selezionare il disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="f35fb-162">Dopo aver selezionato il disco rigido virtuale, fare clic su **OK** per collegare il disco rigido virtuale esistente:</span><span class="sxs-lookup"><span data-stu-id="f35fb-162">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span></span>

    ![Confermare il collegamento del disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="f35fb-164">Dopo alcuni secondi, il riquadro **Dischi** della macchina virtuale esistente mostra il disco rigido virtuale esistente collegato come disco dati:</span><span class="sxs-lookup"><span data-stu-id="f35fb-164">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Disco rigido virtuale esistente collegato come disco dati](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="f35fb-166">Montare il disco dati collegato</span><span class="sxs-lookup"><span data-stu-id="f35fb-166">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="f35fb-167">Gli esempi seguenti mostrano in dettaglio i passaggi necessari in una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f35fb-167">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="f35fb-168">Se si usa una diversa distribuzione Linux, ad esempio Red Hat Enterprise Linux o SUSE, i percorsi dei file di log e i comandi `mount` potrebbero differire.</span><span class="sxs-lookup"><span data-stu-id="f35fb-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="f35fb-169">Consultare la documentazione relativa alla distribuzione specifica per le opportune modifiche ai comandi.</span><span class="sxs-lookup"><span data-stu-id="f35fb-169">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="f35fb-170">Eseguire SSH nella macchina virtuale di cui risolvere i problemi usando le credenziali appropriate.</span><span class="sxs-lookup"><span data-stu-id="f35fb-170">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="f35fb-171">Se questo disco è il primo disco dati collegato alla macchina virtuale di cui risolvere i problemi, è probabilmente connesso a `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="f35fb-171">If this disk is the first data disk attached to your troubleshooting VM, it is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="f35fb-172">Usare `dmseg` per elencare i dischi collegati:</span><span class="sxs-lookup"><span data-stu-id="f35fb-172">Use `dmseg` to list attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="f35fb-173">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f35fb-173">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="f35fb-174">Nell'esempio precedente, il disco del sistema operativo è in `/dev/sda` e il disco temporaneo fornito per ogni macchina virtuale è in `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="f35fb-174">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="f35fb-175">Se sono presenti più dischi dati, devono trovarsi in `/dev/sdd`, `/dev/sde`, e così via.</span><span class="sxs-lookup"><span data-stu-id="f35fb-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="f35fb-176">Creare una directory per montare il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="f35fb-176">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="f35fb-177">L'esempio seguente crea una directory denominata `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="f35fb-177">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="f35fb-178">Se sul disco rigido virtuale esistente sono presenti più partizioni, montare la partizione richiesta.</span><span class="sxs-lookup"><span data-stu-id="f35fb-178">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="f35fb-179">L'esempio seguente monta la prima partizione primaria in `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="f35fb-179">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="f35fb-180">Si consiglia di montare i dischi dati nelle macchine virtuali in Azure usando l'identificatore univoco universale (UUID) del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-180">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="f35fb-181">Per questo scenario, non è necessario montare il disco rigido virtuale usando il relativo l'UUID.</span><span class="sxs-lookup"><span data-stu-id="f35fb-181">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="f35fb-182">Durante il normale utilizzo, invece, modificare `/etc/fstab` per montare i dischi rigidi virtuali usando il nome di dispositivo anziché l'UUID può impedire il corretto avvio della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-182">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="f35fb-183">Risolvere i problemi del disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="f35fb-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="f35fb-184">Dopo aver montato il disco rigido virtuale eseguire tutte le operazioni di manutenzione e i passaggi necessari per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="f35fb-184">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="f35fb-185">Dopo avere risolto i problemi, continuare con la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="f35fb-185">Once you have addressed the issues, continue with the following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="f35fb-186">Smontare e scollegare il disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="f35fb-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="f35fb-187">Dopo aver risolto gli errori, scollegare il disco rigido virtuale esistente dalla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="f35fb-187">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="f35fb-188">Non è possibile usare il disco rigido virtuale con altre macchine virtuali finché non viene rilasciato il lease che collega il disco rigido virtuale alla macchina virtuale usata per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="f35fb-188">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="f35fb-189">Dalla sessione SSH nella macchina virtuale usata per la risoluzione dei problemi, smontare il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="f35fb-189">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="f35fb-190">Modificare innanzitutto la directory padre del punto di montaggio:</span><span class="sxs-lookup"><span data-stu-id="f35fb-190">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="f35fb-191">A questo punto smontare il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="f35fb-191">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="f35fb-192">Nell'esempio viene smontato il dispositivo in `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="f35fb-192">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="f35fb-193">Scollegare il disco rigido virtuale dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-193">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="f35fb-194">Selezionare la macchina virtuale nel portale, quindi fare clic su **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="f35fb-194">Select your VM in the portal and click **Disks**.</span></span> <span data-ttu-id="f35fb-195">Selezionare il disco rigido virtuale esistente quindi fare clic su **Scollega**:</span><span class="sxs-lookup"><span data-stu-id="f35fb-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Scollegare il disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="f35fb-197">Attendere che il disco dati sia completamente scollegato dalla macchina virtuale prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="f35fb-197">Wait until the VM has successfully detached the data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="f35fb-198">Creare una macchina virtuale dal disco rigido originale</span><span class="sxs-lookup"><span data-stu-id="f35fb-198">Create VM from original hard disk</span></span>
<span data-ttu-id="f35fb-199">Per creare una macchina virtuale dal disco rigido virtuale originale, usare [questo modello di Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="f35fb-199">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="f35fb-200">Il modello distribuisce una macchina virtuale in una rete virtuale esistente, usando l'URL del disco rigido virtuale del comando precedente.</span><span class="sxs-lookup"><span data-stu-id="f35fb-200">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="f35fb-201">Fare clic sul pulsante **Distribuisci in Azure** come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f35fb-201">Click the **Deploy to Azure** button as follows:</span></span>

![Distribuire una macchina virtuale da un modello di GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="f35fb-203">Il modello viene caricato nel portale di Azure per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f35fb-203">The template is loaded into the Azure portal for deployment.</span></span> <span data-ttu-id="f35fb-204">Immettere i nomi della nuova macchina virtuale e delle risorse di Azure esistenti e incollare l'URL del disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="f35fb-204">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span></span> <span data-ttu-id="f35fb-205">Per avviare la distribuzione, fare clic su **Acquista**:</span><span class="sxs-lookup"><span data-stu-id="f35fb-205">To begin the deployment, click **Purchase**:</span></span>

![Distribuire una macchina virtuale dal modello](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="f35fb-207">Riabilitare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="f35fb-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="f35fb-208">Quando si crea la macchina virtuale dal disco rigido virtuale esistente, la diagnostica di avvio potrebbe non essere abilitata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f35fb-208">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="f35fb-209">Per controllare lo stato della diagnostica di avvio e attivarla se necessario, selezionare la macchina virtuale nel portale.</span><span class="sxs-lookup"><span data-stu-id="f35fb-209">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span></span> <span data-ttu-id="f35fb-210">In **Monitoraggio**, fare clic su **Impostazioni di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="f35fb-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="f35fb-211">Verificare che lo stato sia **Attivo** e che il segno di spunta accanto a **Diagnostica di avvio** sia selezionato.</span><span class="sxs-lookup"><span data-stu-id="f35fb-211">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span></span> <span data-ttu-id="f35fb-212">Se si apportano modifiche, fare clic su **Salva**:</span><span class="sxs-lookup"><span data-stu-id="f35fb-212">If you make any changes, click **Save**:</span></span>

![Aggiornare le impostazioni di diagnostica di avvio](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="f35fb-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f35fb-214">Next steps</span></span>
<span data-ttu-id="f35fb-215">Se si sono verificati problemi durante la connessione alla macchina virtuale, vedere l'articolo sulla [risoluzione dei problemi di connessione SSH a una macchina virtuale di Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f35fb-215">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f35fb-216">Per problemi relativi all'accesso alle applicazioni in esecuzione nella macchina virtuale, vedere [Risolvere i problemi di connettività delle applicazioni in una macchina virtuale di Azure per Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f35fb-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="f35fb-217">Per altre informazioni sull'uso di Resource Manager, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f35fb-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
