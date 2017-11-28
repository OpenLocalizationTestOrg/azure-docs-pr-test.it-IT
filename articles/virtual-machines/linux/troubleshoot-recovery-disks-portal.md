---
title: aaaUse una risoluzione dei problemi di macchina virtuale nel portale di Azure hello Linux | Documenti Microsoft
description: Informazioni su come i problemi di macchine virtuali Linux tootroubleshoot tramite connessione hello del sistema operativo disco tooa ripristino VM hello portale di Azure
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
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="0be53-103">Risolvere i problemi relativi a una VM Linux tramite il collegamento di ripristino di tooa dischi hello del sistema operativo VM utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0be53-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="0be53-104">Se la macchina virtuale Linux (VM) rileva un errore di avvio o un disco, potrebbe essere tooperform risoluzione dei problemi in disco rigido virtuale hello stesso.</span><span class="sxs-lookup"><span data-stu-id="0be53-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="0be53-105">Un esempio comune sarebbe una voce non valida in `/etc/fstab` che impedisce hello macchina virtuale in grado di tooboot correttamente.</span><span class="sxs-lookup"><span data-stu-id="0be53-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="0be53-106">I dettagli di questo articolo come toouse hello tooconnect portale Azure il virtual hard disco tooanother VM Linux toofix gli eventuali errori, quindi ricreare la macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="0be53-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="0be53-107">Panoramica del processo di ripristino</span><span class="sxs-lookup"><span data-stu-id="0be53-107">Recovery process overview</span></span>
<span data-ttu-id="0be53-108">processo di risoluzione dei problemi di Hello è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0be53-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="0be53-109">Eliminare hello VM rilevati problemi, mantenendo i dischi rigidi virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="0be53-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="0be53-110">Collegare e montare il disco rigido virtuale di hello tooanother VM Linux per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="0be53-110">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="0be53-111">Connettersi toohello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0be53-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="0be53-112">Modificare i file o eseguire gli strumenti toofix problemi del disco rigido virtuale originale di hello.</span><span class="sxs-lookup"><span data-stu-id="0be53-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="0be53-113">Smontare e scollegare hello disco rigido virtuale da hello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0be53-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="0be53-114">Creare una macchina virtuale con disco rigido virtuale originale di hello.</span><span class="sxs-lookup"><span data-stu-id="0be53-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="0be53-115">Individuare i problemi di avvio</span><span class="sxs-lookup"><span data-stu-id="0be53-115">Determine boot issues</span></span>
<span data-ttu-id="0be53-116">Esaminare la diagnostica di avvio hello e VM schermata toodetermine perché la macchina virtuale non è in grado di tooboot correttamente.</span><span class="sxs-lookup"><span data-stu-id="0be53-116">Examine hello boot diagnostics and VM screenshot toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="0be53-117">Un esempio comune è una voce non valida in `/etc/fstab`, oppure l'eliminazione o lo spostamento di un disco rigido virtuale sottostante.</span><span class="sxs-lookup"><span data-stu-id="0be53-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="0be53-118">Selezionare la macchina virtuale nel portale di hello e quindi scorrere verso il basso toohello **supporto + Troubleshooting** sezione.</span><span class="sxs-lookup"><span data-stu-id="0be53-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="0be53-119">Fare clic su **diagnostica di avvio** trasmessi i messaggi della console hello tooview dalla VM.</span><span class="sxs-lookup"><span data-stu-id="0be53-119">Click **Boot diagnostics** tooview hello console messages streamed from your VM.</span></span> <span data-ttu-id="0be53-120">Console hello revisione registra toosee se è possibile determinare perché hello VM sta riscontrando un problema.</span><span class="sxs-lookup"><span data-stu-id="0be53-120">Review hello console logs toosee if you can determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="0be53-121">Hello seguente illustra che una macchina virtuale è bloccata in modalità di manutenzione che richiede l'intervento manuale:</span><span class="sxs-lookup"><span data-stu-id="0be53-121">hello following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Visualizzazione dei registri della console nella diagnostica di avvio della macchina virtuale](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="0be53-123">È anche possibile fare clic su **schermata** in alto hello di hello Avvio diagnostica log toodownload una cattura di schermata di VM hello.</span><span class="sxs-lookup"><span data-stu-id="0be53-123">You can also click **Screenshot** across hello top of hello boot diagnostics log toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="0be53-124">Visualizzare i dettagli del disco rigido virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="0be53-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="0be53-125">Prima di poter allegare i tooanother di disco rigido virtuale a macchina virtuale, è necessario il nome hello tooidentify di hello disco rigido virtuale (VHD).</span><span class="sxs-lookup"><span data-stu-id="0be53-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="0be53-126">Selezionare il gruppo di risorse dal portale di hello, quindi selezionare l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0be53-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="0be53-127">Fare clic su **BLOB**, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="0be53-127">Click **Blobs**, as in hello following example:</span></span>

![Selezionare il BLOB di archiviazione](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="0be53-129">In genere è presente un contenitore denominato **vhds** che contiene i dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="0be53-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="0be53-130">Selezionare hello contenitore tooview un elenco dei dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="0be53-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="0be53-131">Nome della nota hello del disco rigido virtuale (prefisso hello è in genere hello nome della macchina virtuale):</span><span class="sxs-lookup"><span data-stu-id="0be53-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![Identificare il disco rigido virtuale nel contenitore di archiviazione](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="0be53-133">Selezionare il disco rigido virtuale esistente dall'elenco di hello e copiare hello URL per l'utilizzo in hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0be53-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![Copiare l'URL del disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="0be53-135">Eliminare la VM esistente</span><span class="sxs-lookup"><span data-stu-id="0be53-135">Delete existing VM</span></span>
<span data-ttu-id="0be53-136">In Azure, i dischi rigidi virtuali e le macchine virtuali sono due risorse distinte.</span><span class="sxs-lookup"><span data-stu-id="0be53-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="0be53-137">Un disco rigido virtuale è in cui sono archiviate hello sistema operativo, applicazioni e le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="0be53-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="0be53-138">Hello macchina virtuale stessa è esclusivamente i metadati che definisce dimensioni hello o il percorso, quindi fa riferimento a risorse, ad esempio un disco rigido virtuale o di una scheda di interfaccia di rete virtuale (NIC).</span><span class="sxs-lookup"><span data-stu-id="0be53-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="0be53-139">Ogni disco rigido virtuale presenta un lease assegnato quando collegato tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0be53-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="0be53-140">Anche se è possano collegare e scollegare anche durante l'esecuzione di hello VM dischi dati, non è possibile scollegare disco del sistema operativo hello, a meno che non viene eliminato hello risorsa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0be53-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="0be53-141">lease Hello continua il disco del sistema operativo hello tooassociate con una macchina virtuale, anche quando tale macchina virtuale è in uno stato arrestato e deallocato.</span><span class="sxs-lookup"><span data-stu-id="0be53-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="0be53-142">primo passaggio toorecover Hello la macchina virtuale è una risorsa di macchina virtuale hello toodelete stesso.</span><span class="sxs-lookup"><span data-stu-id="0be53-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="0be53-143">L'eliminazione hello VM lascia i dischi rigidi virtuali hello nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0be53-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="0be53-144">Dopo hello che macchina virtuale viene eliminata, collegare hello disco rigido virtuale tooanother VM tootroubleshoot e risolvere gli errori di hello.</span><span class="sxs-lookup"><span data-stu-id="0be53-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="0be53-145">Selezionare la macchina virtuale nel portale di hello, quindi fare clic su **eliminare**:</span><span class="sxs-lookup"><span data-stu-id="0be53-145">Select your VM in hello portal, then click **Delete**:</span></span>

![Schermata di diagnostica di avvio della macchina virtuale che mostra un errore di avvio](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="0be53-147">Attendere il completamento l'eliminazione prima di collegare il disco rigido virtuale di hello tooanother VM hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0be53-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="0be53-148">lease Hello sul disco rigido virtuale hello che associa hello VM deve toobe rilasciati prima di collegare un disco rigido virtuale di hello tooanother macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0be53-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="0be53-149">Collegare tooanother disco rigido virtuale esistente VM</span><span class="sxs-lookup"><span data-stu-id="0be53-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="0be53-150">Per hello successivamente alcuni passaggi, si utilizza un'altra macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="0be53-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="0be53-151">Per collegare toothis disco rigido virtuale esistente hello VM toobe in grado di toobrowse di risoluzione dei problemi e modificare il contenuto del disco hello.</span><span class="sxs-lookup"><span data-stu-id="0be53-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="0be53-152">Questo processo consente toocorrect eventuali errori di configurazione o esame delle applicazioni aggiuntive o file di log, ad esempio system.</span><span class="sxs-lookup"><span data-stu-id="0be53-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="0be53-153">Scegliere o creare un'altra macchina virtuale toouse per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="0be53-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="0be53-154">Selezionare il gruppo di risorse dal portale di hello, quindi selezionare la macchina virtuale di risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="0be53-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="0be53-155">Selezionare **Dischi** e quindi fare clic su **Collega esistente**:</span><span class="sxs-lookup"><span data-stu-id="0be53-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Collegare un disco esistente nel portale di hello](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="0be53-157">tooselect il disco rigido virtuale esistente, fare clic su **File VHD**:</span><span class="sxs-lookup"><span data-stu-id="0be53-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![Cercare il disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="0be53-159">Selezionare l'account e il contenitore di archiviazione, quindi fare clic sul disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="0be53-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="0be53-160">Fare clic su hello **selezionare** pulsante tooconfirm prescelto:</span><span class="sxs-lookup"><span data-stu-id="0be53-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![Selezionare il disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="0be53-162">Con il disco rigido virtuale ora selezionato, fare clic su **OK** tooattach hello disco rigido virtuale esistente:</span><span class="sxs-lookup"><span data-stu-id="0be53-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![Confermare il collegamento del disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="0be53-164">Dopo alcuni secondi, hello **dischi** riquadro per la macchina virtuale sono elencati il disco rigido virtuale esistente collegato come disco dati:</span><span class="sxs-lookup"><span data-stu-id="0be53-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Disco rigido virtuale esistente collegato come disco dati](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="0be53-166">Montare il disco di dati collegato hello</span><span class="sxs-lookup"><span data-stu-id="0be53-166">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="0be53-167">Hello negli esempi seguenti in dettaglio i passaggi di hello necessari in una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="0be53-167">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="0be53-168">Se si utilizza una distribuzione Linux diversi, ad esempio Red Hat Enterprise Linux o SUSE, hello percorsi dei file di log e `mount` comandi potrebbero essere leggermente diversi.</span><span class="sxs-lookup"><span data-stu-id="0be53-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="0be53-169">Consultare la documentazione di toohello per la distribuzione specifiche per le modifiche appropriate hello nei comandi.</span><span class="sxs-lookup"><span data-stu-id="0be53-169">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="0be53-170">Risoluzione dei problemi di macchina virtuale utilizzando le credenziali appropriate hello tooyour SSH.</span><span class="sxs-lookup"><span data-stu-id="0be53-170">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="0be53-171">Se il disco è hello prima dati disco collegato tooyour risoluzione dei problemi di macchina virtuale, è probabilmente connesso troppo`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="0be53-171">If this disk is hello first data disk attached tooyour troubleshooting VM, it is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="0be53-172">Utilizzare `dmseg` toolist dischi collegati:</span><span class="sxs-lookup"><span data-stu-id="0be53-172">Use `dmseg` toolist attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="0be53-173">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="0be53-173">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="0be53-174">In hello sopra riportato, sia su disco del sistema operativo hello `/dev/sda` e disco temporaneo di hello fornito per ogni macchina virtuale è in `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="0be53-174">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="0be53-175">Se sono presenti più dischi dati, devono trovarsi in `/dev/sdd`, `/dev/sde`, e così via.</span><span class="sxs-lookup"><span data-stu-id="0be53-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="0be53-176">Creare una directory toomount il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="0be53-176">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="0be53-177">esempio Hello crea una directory denominata `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="0be53-177">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="0be53-178">Se si dispone di più partizioni sul disco rigido virtuale esistente, è possibile montare partizione hello necessario.</span><span class="sxs-lookup"><span data-stu-id="0be53-178">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="0be53-179">esempio Hello Monta prima partizione primaria hello in `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="0be53-179">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="0be53-180">È consigliabile che i dischi dati toomount nelle macchine virtuali in Azure tramite hello identificatore univoco universale (UUID) del disco rigido virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="0be53-180">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="0be53-181">Per questo scenario di risoluzione dei problemi breve, il montaggio hello disco rigido virtuale eseguendo hello UUID non è necessario.</span><span class="sxs-lookup"><span data-stu-id="0be53-181">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="0be53-182">Tuttavia, il normale utilizzo, la modifica `/etc/fstab` dischi rigidi virtuali toomount utilizzando il nome di dispositivo anziché potrebbe provocare l'UUID hello tooboot toofail macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0be53-182">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="0be53-183">Risolvere i problemi del disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="0be53-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="0be53-184">Con hello esistente disco rigido virtuale montato, è ora possibile eseguire operazioni di manutenzione e risoluzione dei problemi in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="0be53-184">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="0be53-185">Dopo avere risolto i problemi di hello, continuare con hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="0be53-185">Once you have addressed hello issues, continue with hello following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="0be53-186">Smontare e scollegare il disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="0be53-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="0be53-187">Una volta risolti gli errori, scollegare hello disco rigido virtuale esistente dalla VM sulla risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="0be53-187">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="0be53-188">È possibile utilizzare il disco rigido virtuale con qualsiasi altra macchina virtuale finché non viene rilasciato il lease hello collegamento hello disco rigido virtuale toohello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0be53-188">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="0be53-189">Da hello SSH sessione tooyour risoluzione dei problemi di macchina virtuale, effettuare lo smontaggio hello disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="0be53-189">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="0be53-190">Modificare innanzitutto dalla directory padre hello per il punto di montaggio:</span><span class="sxs-lookup"><span data-stu-id="0be53-190">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="0be53-191">Smonta ora hello disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="0be53-191">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="0be53-192">esempio Hello Smonta dispositivo hello `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="0be53-192">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="0be53-193">Scollegare ora hello disco rigido virtuale dalla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="0be53-193">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="0be53-194">Selezionare la macchina virtuale nel portale di hello e fare clic su **dischi**.</span><span class="sxs-lookup"><span data-stu-id="0be53-194">Select your VM in hello portal and click **Disks**.</span></span> <span data-ttu-id="0be53-195">Selezionare il disco rigido virtuale esistente quindi fare clic su **Scollega**:</span><span class="sxs-lookup"><span data-stu-id="0be53-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Scollegare il disco rigido virtuale esistente](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="0be53-197">Attendere hello VM è stato scollegato disco dati hello prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="0be53-197">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="0be53-198">Creare una macchina virtuale dal disco rigido originale</span><span class="sxs-lookup"><span data-stu-id="0be53-198">Create VM from original hard disk</span></span>
<span data-ttu-id="0be53-199">utilizzare una macchina virtuale dal disco rigido virtuale originale, toocreate [questo modello di gestione risorse di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="0be53-199">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="0be53-200">modello Hello distribuisce una macchina virtuale in una rete virtuale esistente, utilizzando il messaggio hello URL VHD from hello in precedenza di comando.</span><span class="sxs-lookup"><span data-stu-id="0be53-200">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="0be53-201">Fare clic su hello **distribuire tooAzure** pulsante come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0be53-201">Click hello **Deploy tooAzure** button as follows:</span></span>

![Distribuire una macchina virtuale da un modello di GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="0be53-203">modello Hello viene caricata in hello portale di Azure per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0be53-203">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="0be53-204">Immettere un nome hello per la nuova macchina virtuale e le risorse di Azure esistente e incollare hello URL tooyour disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="0be53-204">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="0be53-205">distribuzione di hello toobegin, fare clic su **acquisto**:</span><span class="sxs-lookup"><span data-stu-id="0be53-205">toobegin hello deployment, click **Purchase**:</span></span>

![Distribuire una macchina virtuale dal modello](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="0be53-207">Riabilitare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="0be53-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="0be53-208">Quando si crea la macchina virtuale dal disco rigido virtuale esistente di hello, la diagnostica di avvio potrebbe non essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0be53-208">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="0be53-209">toocheck hello lo stato di diagnostica di avvio e attivare se necessario, selezionare la macchina virtuale nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="0be53-209">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="0be53-210">In **Monitoraggio**, fare clic su **Impostazioni di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="0be53-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="0be53-211">Verificare che sia stato hello **su**, e hello segno di spunta accanto troppo**diagnostica di avvio** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="0be53-211">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="0be53-212">Se si apportano modifiche, fare clic su **Salva**:</span><span class="sxs-lookup"><span data-stu-id="0be53-212">If you make any changes, click **Save**:</span></span>

![Aggiornare le impostazioni di diagnostica di avvio](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="0be53-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0be53-214">Next steps</span></span>
<span data-ttu-id="0be53-215">Se si sono verificati problemi di connessione tooyour VM, vedere [tooan connessioni risolvere SSH macchina virtuale di Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0be53-215">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0be53-216">Per problemi relativi all'accesso alle applicazioni in esecuzione nella macchina virtuale, vedere [Risolvere i problemi di connettività delle applicazioni in una macchina virtuale di Azure per Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0be53-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0be53-217">Per altre informazioni sull'uso di Resource Manager, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0be53-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
