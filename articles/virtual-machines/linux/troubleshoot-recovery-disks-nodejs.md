---
title: aaaUse una risoluzione dei problemi di VM con hello Azure CLI 1.0 Linux | Documenti Microsoft
description: Informazioni su come tootroubleshoot VM Linux problemi tramite connessione hello del sistema operativo disco tooa ripristino VM hello Azure CLI 1.0
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
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a><span data-ttu-id="c3c81-103">Risolvere i problemi relativi a una VM Linux tramite il collegamento di ripristino di tooa dischi hello del sistema operativo VM utilizzando hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c3c81-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="c3c81-104">Se la macchina virtuale Linux (VM) rileva un errore di avvio o un disco, potrebbe essere tooperform risoluzione dei problemi in disco rigido virtuale hello stesso.</span><span class="sxs-lookup"><span data-stu-id="c3c81-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="c3c81-105">Un esempio comune sarebbe una voce non valida in `/etc/fstab` che impedisce hello macchina virtuale in grado di tooboot correttamente.</span><span class="sxs-lookup"><span data-stu-id="c3c81-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="c3c81-106">I dettagli di questo articolo come toouse hello tooconnect CLI di Azure 1.0 il virtual hard disco tooanother VM Linux toofix gli eventuali errori, quindi ricreare la macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-106">This article details how toouse hello Azure CLI 1.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="c3c81-107">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="c3c81-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="c3c81-108">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="c3c81-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="c3c81-109">[Azure CLI 1.0](#recovery-process-overview) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="c3c81-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c3c81-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="c3c81-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="c3c81-111">Panoramica del processo di ripristino</span><span class="sxs-lookup"><span data-stu-id="c3c81-111">Recovery process overview</span></span>
<span data-ttu-id="c3c81-112">processo di risoluzione dei problemi di Hello è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c3c81-112">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="c3c81-113">Eliminare hello VM rilevati problemi, mantenendo i dischi rigidi virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="c3c81-113">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="c3c81-114">Collegare e montare il disco rigido virtuale di hello tooanother VM Linux per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="c3c81-114">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="c3c81-115">Connettersi toohello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-115">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="c3c81-116">Modificare i file o eseguire gli strumenti toofix problemi del disco rigido virtuale originale di hello.</span><span class="sxs-lookup"><span data-stu-id="c3c81-116">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="c3c81-117">Smontare e scollegare hello disco rigido virtuale da hello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-117">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="c3c81-118">Creare una macchina virtuale con disco rigido virtuale originale di hello.</span><span class="sxs-lookup"><span data-stu-id="c3c81-118">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="c3c81-119">Assicurarsi di aver [hello più recente di Azure CLI 1.0](../../cli-install-nodejs.md) installati e registrati e utilizza la modalità di gestione delle risorse:</span><span class="sxs-lookup"><span data-stu-id="c3c81-119">Make sure that you have [hello latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="c3c81-120">In hello negli esempi seguenti, sostituire i nomi dei parametri con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="c3c81-120">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="c3c81-121">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="c3c81-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="c3c81-122">Individuare i problemi di avvio</span><span class="sxs-lookup"><span data-stu-id="c3c81-122">Determine boot issues</span></span>
<span data-ttu-id="c3c81-123">Esaminare hello output seriale toodetermine perché la macchina virtuale non è in grado di tooboot correttamente.</span><span class="sxs-lookup"><span data-stu-id="c3c81-123">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="c3c81-124">Un esempio comune è una voce non valida in `/etc/fstab`, o hello sottostante il disco rigido virtuale viene eliminato o spostato.</span><span class="sxs-lookup"><span data-stu-id="c3c81-124">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="c3c81-125">Hello seguente esempio mostra come ottenere output seriale hello dalla macchina virtuale denominata hello `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c3c81-125">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="c3c81-126">Esaminare hello output seriale toodetermine hello VM motivi tooboot.</span><span class="sxs-lookup"><span data-stu-id="c3c81-126">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="c3c81-127">Se l'output di hello seriale non fornisce alcuna indicazione, potrebbe essere necessario tooreview i file di log in `/var/log` dopo aver hello virtuale disco rigido connesso tooa risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-127">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="c3c81-128">Visualizzare i dettagli del disco rigido virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="c3c81-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="c3c81-129">Prima di poter allegare i tooanother di disco rigido virtuale a macchina virtuale, è necessario il nome hello tooidentify di hello disco rigido virtuale (VHD).</span><span class="sxs-lookup"><span data-stu-id="c3c81-129">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="c3c81-130">Hello seguente esempio mostra come ottenere informazioni per la macchina virtuale denominata hello `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c3c81-130">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="c3c81-131">Cercare `Vhd URI` nell'output di hello da hello precedente comando.</span><span class="sxs-lookup"><span data-stu-id="c3c81-131">Look for `Vhd URI` in hello output from hello preceding command.</span></span> <span data-ttu-id="c3c81-132">output di esempio troncato seguente Hello Mostra hello `Vhd URI` ultima riga hello:</span><span class="sxs-lookup"><span data-stu-id="c3c81-132">hello following truncated example output shows hello `Vhd URI` on hello last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
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


## <a name="delete-existing-vm"></a><span data-ttu-id="c3c81-133">Eliminare la VM esistente</span><span class="sxs-lookup"><span data-stu-id="c3c81-133">Delete existing VM</span></span>
<span data-ttu-id="c3c81-134">In Azure, i dischi rigidi virtuali e le macchine virtuali sono due risorse distinte.</span><span class="sxs-lookup"><span data-stu-id="c3c81-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="c3c81-135">Un disco rigido virtuale è in cui sono archiviate hello sistema operativo, applicazioni e le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="c3c81-135">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="c3c81-136">Hello macchina virtuale stessa è esclusivamente i metadati che definisce dimensioni hello o il percorso, quindi fa riferimento a risorse, ad esempio un disco rigido virtuale o di una scheda di interfaccia di rete virtuale (NIC).</span><span class="sxs-lookup"><span data-stu-id="c3c81-136">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="c3c81-137">Ogni disco rigido virtuale presenta un lease assegnato quando collegato tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-137">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="c3c81-138">Anche se è possano collegare e scollegare anche durante l'esecuzione di hello VM dischi dati, non è possibile scollegare disco del sistema operativo hello, a meno che non viene eliminato hello risorsa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-138">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="c3c81-139">lease Hello continua il disco del sistema operativo hello tooassociate con una macchina virtuale, anche quando tale macchina virtuale è in uno stato arrestato e deallocato.</span><span class="sxs-lookup"><span data-stu-id="c3c81-139">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="c3c81-140">primo passaggio toorecover Hello la macchina virtuale è una risorsa di macchina virtuale hello toodelete stesso.</span><span class="sxs-lookup"><span data-stu-id="c3c81-140">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="c3c81-141">L'eliminazione hello VM lascia i dischi rigidi virtuali hello nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c3c81-141">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="c3c81-142">Dopo hello che macchina virtuale viene eliminata, collegare hello disco rigido virtuale tooanother VM tootroubleshoot e risolvere gli errori di hello.</span><span class="sxs-lookup"><span data-stu-id="c3c81-142">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="c3c81-143">Hello seguente esempio vengono eliminate hello macchina virtuale denominata `myVM` dal gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c3c81-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="c3c81-144">Attendere il completamento l'eliminazione prima di collegare il disco rigido virtuale di hello tooanother VM hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="c3c81-145">lease Hello sul disco rigido virtuale hello che associa hello VM deve toobe rilasciati prima di collegare un disco rigido virtuale di hello tooanother macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="c3c81-146">Collegare tooanother disco rigido virtuale esistente VM</span><span class="sxs-lookup"><span data-stu-id="c3c81-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="c3c81-147">Per hello successivamente alcuni passaggi, si utilizza un'altra macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="c3c81-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="c3c81-148">Per collegare hello toothis di disco rigido virtuale esistente toobrowse VM di risoluzione dei problemi e modificare il contenuto del disco hello.</span><span class="sxs-lookup"><span data-stu-id="c3c81-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="c3c81-149">Questo processo consente toocorrect eventuali errori di configurazione o esame delle applicazioni aggiuntive o file di log, ad esempio system.</span><span class="sxs-lookup"><span data-stu-id="c3c81-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="c3c81-150">Scegliere o creare un'altra macchina virtuale toouse per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="c3c81-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="c3c81-151">Quando si collega hello disco rigido virtuale esistente, specificare disco toohello di URL hello ottenuto in precedenza hello `azure vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="c3c81-151">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `azure vm show` command.</span></span> <span data-ttu-id="c3c81-152">esempio Hello collega un toohello disco rigido virtuale esistente, risoluzione dei problemi di macchina virtuale denominata `myVMRecovery` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c3c81-152">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="c3c81-153">Montare il disco di dati collegato hello</span><span class="sxs-lookup"><span data-stu-id="c3c81-153">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="c3c81-154">Hello negli esempi seguenti in dettaglio i passaggi di hello necessari in una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c3c81-154">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="c3c81-155">Se si utilizza una distribuzione Linux diversi, ad esempio Red Hat Enterprise Linux o SUSE, hello percorsi dei file di log e `mount` comandi potrebbero essere leggermente diversi.</span><span class="sxs-lookup"><span data-stu-id="c3c81-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="c3c81-156">Consultare la documentazione di toohello per la distribuzione specifiche per le modifiche appropriate hello nei comandi.</span><span class="sxs-lookup"><span data-stu-id="c3c81-156">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="c3c81-157">Risoluzione dei problemi di macchina virtuale utilizzando le credenziali appropriate hello tooyour SSH.</span><span class="sxs-lookup"><span data-stu-id="c3c81-157">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="c3c81-158">Se il disco è hello prima dati disco collegato tooyour risoluzione dei problemi di macchina virtuale, disco hello è probabilmente connesso troppo`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="c3c81-158">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="c3c81-159">Utilizzare `dmseg` tooview dischi collegati:</span><span class="sxs-lookup"><span data-stu-id="c3c81-159">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="c3c81-160">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="c3c81-160">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="c3c81-161">In hello sopra riportato, sia su disco del sistema operativo hello `/dev/sda` e disco temporaneo di hello fornito per ogni macchina virtuale è in `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="c3c81-161">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="c3c81-162">Se sono presenti più dischi dati, devono trovarsi in `/dev/sdd`, `/dev/sde`, e così via.</span><span class="sxs-lookup"><span data-stu-id="c3c81-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="c3c81-163">Creare una directory toomount il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="c3c81-163">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="c3c81-164">esempio Hello crea una directory denominata `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="c3c81-164">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="c3c81-165">Se si dispone di più partizioni sul disco rigido virtuale esistente, è possibile montare partizione hello necessario.</span><span class="sxs-lookup"><span data-stu-id="c3c81-165">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="c3c81-166">esempio Hello Monta prima partizione primaria hello in `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="c3c81-166">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="c3c81-167">È consigliabile che i dischi dati toomount nelle macchine virtuali in Azure tramite hello identificatore univoco universale (UUID) del disco rigido virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c3c81-167">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="c3c81-168">Per questo scenario di risoluzione dei problemi breve, il montaggio hello disco rigido virtuale eseguendo hello UUID non è necessario.</span><span class="sxs-lookup"><span data-stu-id="c3c81-168">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="c3c81-169">Tuttavia, il normale utilizzo, la modifica `/etc/fstab` dischi rigidi virtuali toomount utilizzando il nome di dispositivo anziché potrebbe provocare l'UUID hello tooboot toofail macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-169">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="c3c81-170">Risolvere i problemi del disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="c3c81-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="c3c81-171">Con hello esistente disco rigido virtuale montato, è ora possibile eseguire operazioni di manutenzione e risoluzione dei problemi in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="c3c81-171">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="c3c81-172">Dopo avere risolto i problemi di hello, continuare con hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="c3c81-172">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="c3c81-173">Smontare e scollegare il disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="c3c81-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="c3c81-174">Una volta risolti gli errori, si smontare e Scollega hello disco rigido virtuale esistente dalla VM sulla risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="c3c81-174">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="c3c81-175">È possibile utilizzare il disco rigido virtuale con qualsiasi altra macchina virtuale finché non viene rilasciato il lease hello collegamento hello disco rigido virtuale toohello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-175">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="c3c81-176">Da hello SSH sessione tooyour risoluzione dei problemi di macchina virtuale, effettuare lo smontaggio hello disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="c3c81-176">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="c3c81-177">Modificare innanzitutto dalla directory padre hello per il punto di montaggio:</span><span class="sxs-lookup"><span data-stu-id="c3c81-177">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="c3c81-178">Smonta ora hello disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="c3c81-178">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="c3c81-179">esempio Hello Smonta dispositivo hello `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="c3c81-179">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="c3c81-180">Scollegare ora hello disco rigido virtuale dalla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c3c81-180">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="c3c81-181">Uscire da hello SSH sessione tooyour risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-181">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="c3c81-182">In hello CLI di Azure, hello elenco primo allegato tooyour dischi dati risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-182">In hello Azure CLI, first list hello attached data disks tooyour troubleshooting VM.</span></span> <span data-ttu-id="c3c81-183">gli elenchi di hello dischi dati di esempio seguente Hello collegato toohello macchina virtuale denominata `myVMRecovery` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c3c81-183">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="c3c81-184">Hello nota `Lun` valore per il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="c3c81-184">Note hello `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="c3c81-185">Hello output di comando di esempio seguente mostra hello disco virtuale collegato al LUN 0:</span><span class="sxs-lookup"><span data-stu-id="c3c81-185">hello following example command output shows hello existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="c3c81-186">Scollegare il disco dati hello dalla VM utilizzando hello applicabile `Lun` valore:</span><span class="sxs-lookup"><span data-stu-id="c3c81-186">Detach hello data disk from your VM using hello applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="c3c81-187">Creare una macchina virtuale dal disco rigido originale</span><span class="sxs-lookup"><span data-stu-id="c3c81-187">Create VM from original hard disk</span></span>
<span data-ttu-id="c3c81-188">utilizzare una macchina virtuale dal disco rigido virtuale originale, toocreate [questo modello di gestione risorse di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="c3c81-188">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="c3c81-189">modello JSON effettivi Hello è hello link riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c3c81-189">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="c3c81-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c3c81-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="c3c81-191">modello Hello distribuisce una macchina virtuale in una rete virtuale esistente, utilizzando il messaggio hello URL VHD from hello in precedenza di comando.</span><span class="sxs-lookup"><span data-stu-id="c3c81-191">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="c3c81-192">esempio Hello distribuisce hello modello toohello gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c3c81-192">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="c3c81-193">Hello risposta richiesto per il modello di hello ad esempio nome della macchina virtuale (`myDeployedVM` hello seguente esempio), tipo di sistema operativo (`Linux`) e le dimensioni di macchina virtuale (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="c3c81-193">Answer hello prompts for hello template such as VM name (`myDeployedVM` hello following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="c3c81-194">Hello `osDiskVhdUri` è hello stesso utilizzato in precedenza durante l'associazione toohello disco rigido virtuale esistente hello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c3c81-194">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span> <span data-ttu-id="c3c81-195">Un esempio di output del comando hello e richieste è il seguente:</span><span class="sxs-lookup"><span data-stu-id="c3c81-195">An example of hello command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
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
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="c3c81-196">Riabilitare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="c3c81-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="c3c81-197">Quando si crea la macchina virtuale dal disco rigido virtuale esistente di hello, la diagnostica di avvio potrebbe non essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c3c81-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="c3c81-198">esempio Hello consente hello un'estensione di diagnostica nella macchina virtuale denominata hello `myDeployedVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c3c81-198">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="c3c81-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c3c81-199">Next steps</span></span>
<span data-ttu-id="c3c81-200">Se si sono verificati problemi di connessione tooyour VM, vedere [tooan connessioni risolvere SSH macchina virtuale di Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c3c81-200">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c3c81-201">Per problemi relativi all'accesso alle applicazioni in esecuzione nella macchina virtuale, vedere [Risolvere i problemi di connettività delle applicazioni in una macchina virtuale di Azure per Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c3c81-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
