---
title: aaaUse una risoluzione dei problemi di VM con hello Azure CLI 2.0 Linux | Documenti Microsoft
description: Informazioni su come tootroubleshoot VM Linux problemi tramite connessione hello del sistema operativo disco tooa ripristino VM hello Azure CLI 2.0
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
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a><span data-ttu-id="10ec8-103">Risolvere i problemi relativi a una VM Linux tramite il collegamento di ripristino tooa hello del sistema operativo del disco VM con hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="10ec8-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM with hello Azure CLI 2.0</span></span>
<span data-ttu-id="10ec8-104">Se la macchina virtuale Linux (VM) rileva un errore di avvio o un disco, potrebbe essere tooperform risoluzione dei problemi in disco rigido virtuale hello stesso.</span><span class="sxs-lookup"><span data-stu-id="10ec8-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="10ec8-105">Un esempio comune sarebbe una voce non valida in `/etc/fstab` che impedisce hello macchina virtuale in grado di tooboot correttamente.</span><span class="sxs-lookup"><span data-stu-id="10ec8-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="10ec8-106">I dettagli di questo articolo come toouse hello tooconnect CLI di Azure 2.0 il virtual hard disco tooanother VM Linux toofix gli eventuali errori, quindi ricreare la macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="10ec8-106">This article details how toouse hello Azure CLI 2.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span> <span data-ttu-id="10ec8-107">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10ec8-107">You can also perform these steps with hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="10ec8-108">Panoramica del processo di ripristino</span><span class="sxs-lookup"><span data-stu-id="10ec8-108">Recovery process overview</span></span>
<span data-ttu-id="10ec8-109">processo di risoluzione dei problemi di Hello è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="10ec8-109">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="10ec8-110">Eliminare hello VM rilevati problemi, mantenendo i dischi rigidi virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="10ec8-110">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="10ec8-111">Collegare e montare il disco rigido virtuale di hello tooanother VM Linux per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="10ec8-111">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="10ec8-112">Connettersi toohello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10ec8-112">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="10ec8-113">Modificare i file o eseguire gli strumenti toofix problemi del disco rigido virtuale originale di hello.</span><span class="sxs-lookup"><span data-stu-id="10ec8-113">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="10ec8-114">Smontare e scollegare hello disco rigido virtuale da hello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10ec8-114">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="10ec8-115">Creare una macchina virtuale con disco rigido virtuale originale di hello.</span><span class="sxs-lookup"><span data-stu-id="10ec8-115">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="10ec8-116">tooperform passaggi di risoluzione dei problemi è necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="10ec8-116">tooperform these troubleshooting steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="10ec8-117">In hello negli esempi seguenti, sostituire i nomi dei parametri con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="10ec8-117">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="10ec8-118">I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="10ec8-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="10ec8-119">Individuare i problemi di avvio</span><span class="sxs-lookup"><span data-stu-id="10ec8-119">Determine boot issues</span></span>
<span data-ttu-id="10ec8-120">Esaminare hello output seriale toodetermine perché la macchina virtuale non è in grado di tooboot correttamente.</span><span class="sxs-lookup"><span data-stu-id="10ec8-120">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="10ec8-121">Un esempio comune è una voce non valida in `/etc/fstab`, o hello sottostante il disco rigido virtuale viene eliminato o spostato.</span><span class="sxs-lookup"><span data-stu-id="10ec8-121">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="10ec8-122">Ottenere i log di avvio hello con [az vm get diagnostica di avvio-avvio-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="10ec8-122">Get hello boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="10ec8-123">Hello seguente esempio mostra come ottenere output seriale hello dalla macchina virtuale denominata hello `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="10ec8-123">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="10ec8-124">Esaminare hello output seriale toodetermine hello VM motivi tooboot.</span><span class="sxs-lookup"><span data-stu-id="10ec8-124">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="10ec8-125">Se l'output di hello seriale non fornisce alcuna indicazione, potrebbe essere necessario tooreview i file di log in `/var/log` dopo aver hello virtuale disco rigido connesso tooa risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10ec8-125">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="10ec8-126">Visualizzare i dettagli del disco rigido virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="10ec8-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="10ec8-127">Prima di collegare la macchina virtuale di tooanother di disco rigido virtuale (VHD), è necessario tooidentify hello URI del disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="10ec8-127">Before you can attach your virtual hard disk (VHD) tooanother VM, you need tooidentify hello URI of hello OS disk.</span></span> 

<span data-ttu-id="10ec8-128">Visualizzare le informazioni sulla macchina virtuale con il comando [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="10ec8-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="10ec8-129">Hello utilizzare `--query` disco toohello del sistema operativo di flag tooextract hello URI.</span><span class="sxs-lookup"><span data-stu-id="10ec8-129">Use hello `--query` flag tooextract hello URI toohello OS disk.</span></span> <span data-ttu-id="10ec8-130">esempio Hello Ottiene informazioni sul disco per la macchina virtuale denominata hello `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="10ec8-130">hello following example gets disk information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="10ec8-131">Hello URI è simile a troppo**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="10ec8-131">hello URI is similar too**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="10ec8-132">Eliminare la VM esistente</span><span class="sxs-lookup"><span data-stu-id="10ec8-132">Delete existing VM</span></span>
<span data-ttu-id="10ec8-133">In Azure, i dischi rigidi virtuali e le macchine virtuali sono due risorse distinte.</span><span class="sxs-lookup"><span data-stu-id="10ec8-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="10ec8-134">Un disco rigido virtuale è in cui sono archiviate hello sistema operativo, applicazioni e le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="10ec8-134">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="10ec8-135">Hello macchina virtuale stessa è esclusivamente i metadati che definisce dimensioni hello o il percorso, quindi fa riferimento a risorse, ad esempio un disco rigido virtuale o di una scheda di interfaccia di rete virtuale (NIC).</span><span class="sxs-lookup"><span data-stu-id="10ec8-135">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="10ec8-136">Ogni disco rigido virtuale presenta un lease assegnato quando collegato tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10ec8-136">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="10ec8-137">Anche se è possano collegare e scollegare anche durante l'esecuzione di hello VM dischi dati, non è possibile scollegare disco del sistema operativo hello, a meno che non viene eliminato hello risorsa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10ec8-137">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="10ec8-138">lease Hello continua il disco del sistema operativo hello tooassociate con una macchina virtuale, anche quando tale macchina virtuale è in uno stato arrestato e deallocato.</span><span class="sxs-lookup"><span data-stu-id="10ec8-138">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="10ec8-139">primo passaggio toorecover Hello la macchina virtuale è una risorsa di macchina virtuale hello toodelete stesso.</span><span class="sxs-lookup"><span data-stu-id="10ec8-139">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="10ec8-140">L'eliminazione hello VM lascia i dischi rigidi virtuali hello nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="10ec8-140">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="10ec8-141">Dopo hello che macchina virtuale viene eliminata, collegare hello disco rigido virtuale tooanother VM tootroubleshoot e risolvere gli errori di hello.</span><span class="sxs-lookup"><span data-stu-id="10ec8-141">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="10ec8-142">Elimina macchina virtuale con hello [az vm eliminare](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="10ec8-142">Delete hello VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="10ec8-143">Hello seguente esempio vengono eliminate hello macchina virtuale denominata `myVM` dal gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="10ec8-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="10ec8-144">Attendere il completamento l'eliminazione prima di collegare il disco rigido virtuale di hello tooanother VM hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10ec8-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="10ec8-145">lease Hello sul disco rigido virtuale hello che associa hello VM deve toobe rilasciati prima di collegare un disco rigido virtuale di hello tooanother macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10ec8-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="10ec8-146">Collegare tooanother disco rigido virtuale esistente VM</span><span class="sxs-lookup"><span data-stu-id="10ec8-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="10ec8-147">Per hello successivamente alcuni passaggi, si utilizza un'altra macchina virtuale per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="10ec8-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="10ec8-148">Per collegare hello toothis di disco rigido virtuale esistente toobrowse VM di risoluzione dei problemi e modificare il contenuto del disco hello.</span><span class="sxs-lookup"><span data-stu-id="10ec8-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="10ec8-149">Questo processo consente toocorrect eventuali errori di configurazione o esame delle applicazioni aggiuntive o file di log, ad esempio system.</span><span class="sxs-lookup"><span data-stu-id="10ec8-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="10ec8-150">Scegliere o creare un'altra macchina virtuale toouse per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="10ec8-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="10ec8-151">Collegare hello disco rigido virtuale esistente con [az disco macchina virtuale non gestita-collegare](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="10ec8-151">Attach hello existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="10ec8-152">Quando si collega hello disco rigido virtuale esistente, specificare disco toohello URI hello ottenuto in precedenza hello `az vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="10ec8-152">When you attach hello existing virtual hard disk, specify hello URI toohello disk obtained in hello preceding `az vm show` command.</span></span> <span data-ttu-id="10ec8-153">esempio Hello collega un toohello disco rigido virtuale esistente, risoluzione dei problemi di macchina virtuale denominata `myVMRecovery` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="10ec8-153">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="10ec8-154">Montare il disco di dati collegato hello</span><span class="sxs-lookup"><span data-stu-id="10ec8-154">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="10ec8-155">Hello negli esempi seguenti in dettaglio i passaggi di hello necessari in una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="10ec8-155">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="10ec8-156">Se si utilizza una distribuzione Linux diversi, ad esempio Red Hat Enterprise Linux o SUSE, hello percorsi dei file di log e `mount` comandi potrebbero essere leggermente diversi.</span><span class="sxs-lookup"><span data-stu-id="10ec8-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="10ec8-157">Consultare la documentazione di toohello per la distribuzione specifiche per le modifiche appropriate hello nei comandi.</span><span class="sxs-lookup"><span data-stu-id="10ec8-157">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="10ec8-158">Risoluzione dei problemi di macchina virtuale utilizzando le credenziali appropriate hello tooyour SSH.</span><span class="sxs-lookup"><span data-stu-id="10ec8-158">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="10ec8-159">Se il disco è hello prima dati disco collegato tooyour risoluzione dei problemi di macchina virtuale, disco hello è probabilmente connesso troppo`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="10ec8-159">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="10ec8-160">Utilizzare `dmseg` tooview dischi collegati:</span><span class="sxs-lookup"><span data-stu-id="10ec8-160">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="10ec8-161">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="10ec8-161">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="10ec8-162">In hello sopra riportato, sia su disco del sistema operativo hello `/dev/sda` e disco temporaneo di hello fornito per ogni macchina virtuale è in `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="10ec8-162">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="10ec8-163">Se sono presenti più dischi dati, devono trovarsi in `/dev/sdd`, `/dev/sde`, e così via.</span><span class="sxs-lookup"><span data-stu-id="10ec8-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="10ec8-164">Creare una directory toomount il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="10ec8-164">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="10ec8-165">esempio Hello crea una directory denominata `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="10ec8-165">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="10ec8-166">Se si dispone di più partizioni sul disco rigido virtuale esistente, è possibile montare partizione hello necessario.</span><span class="sxs-lookup"><span data-stu-id="10ec8-166">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="10ec8-167">esempio Hello Monta prima partizione primaria hello in `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="10ec8-167">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="10ec8-168">È consigliabile che i dischi dati toomount nelle macchine virtuali in Azure tramite hello identificatore univoco universale (UUID) del disco rigido virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="10ec8-168">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="10ec8-169">Per questo scenario di risoluzione dei problemi breve, il montaggio hello disco rigido virtuale eseguendo hello UUID non è necessario.</span><span class="sxs-lookup"><span data-stu-id="10ec8-169">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="10ec8-170">Tuttavia, il normale utilizzo, la modifica `/etc/fstab` dischi rigidi virtuali toomount utilizzando il nome di dispositivo anziché potrebbe provocare l'UUID hello tooboot toofail macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10ec8-170">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="10ec8-171">Risolvere i problemi del disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="10ec8-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="10ec8-172">Con hello esistente disco rigido virtuale montato, è ora possibile eseguire operazioni di manutenzione e risoluzione dei problemi in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="10ec8-172">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="10ec8-173">Dopo avere risolto i problemi di hello, continuare con hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="10ec8-173">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="10ec8-174">Smontare e scollegare il disco rigido virtuale originale</span><span class="sxs-lookup"><span data-stu-id="10ec8-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="10ec8-175">Una volta risolti gli errori, si smontare e Scollega hello disco rigido virtuale esistente dalla VM sulla risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="10ec8-175">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="10ec8-176">È possibile utilizzare il disco rigido virtuale con qualsiasi altra macchina virtuale finché non viene rilasciato il lease hello collegamento hello disco rigido virtuale toohello risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10ec8-176">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="10ec8-177">Da hello SSH sessione tooyour risoluzione dei problemi di macchina virtuale, effettuare lo smontaggio hello disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="10ec8-177">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="10ec8-178">Modificare innanzitutto dalla directory padre hello per il punto di montaggio:</span><span class="sxs-lookup"><span data-stu-id="10ec8-178">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="10ec8-179">Smonta ora hello disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="10ec8-179">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="10ec8-180">esempio Hello Smonta dispositivo hello `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="10ec8-180">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="10ec8-181">Scollegare ora hello disco rigido virtuale dalla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="10ec8-181">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="10ec8-182">Uscire da hello SSH sessione tooyour risoluzione dei problemi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10ec8-182">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="10ec8-183">Hello elenco collegato tooyour dischi dati risoluzione dei problemi di macchina virtuale con [elenco disco non gestita di vm az](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="10ec8-183">List hello attached data disks tooyour troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="10ec8-184">gli elenchi di hello dischi dati di esempio seguente Hello collegato toohello macchina virtuale denominata `myVMRecovery` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="10ec8-184">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="10ec8-185">Si noti il nome di hello per il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="10ec8-185">Note hello name for your existing virtual hard disk.</span></span> <span data-ttu-id="10ec8-186">Ad esempio, il nome di hello di un disco con hello URI di **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** è **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="10ec8-186">For example, hello name of a disk with hello URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="10ec8-187">Scollegare il disco dati hello dalla VM [az vm non gestita disco scollegare](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="10ec8-187">Detach hello data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="10ec8-188">esempio Hello Scollega disco hello denominato `myVHD` dalla macchina virtuale denominata hello `myVMRecovery` in hello `myResourceGroup` gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="10ec8-188">hello following example detaches hello disk named `myVHD` from hello VM named `myVMRecovery` in hello `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="10ec8-189">Creare una macchina virtuale dal disco rigido originale</span><span class="sxs-lookup"><span data-stu-id="10ec8-189">Create VM from original hard disk</span></span>
<span data-ttu-id="10ec8-190">utilizzare una macchina virtuale dal disco rigido virtuale originale, toocreate [questo modello di gestione risorse di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="10ec8-190">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="10ec8-191">modello JSON effettivi Hello è hello link riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="10ec8-191">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="10ec8-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="10ec8-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="10ec8-193">modello Hello distribuisce una macchina virtuale tramite hello URI VHD da hello in precedenza di comando.</span><span class="sxs-lookup"><span data-stu-id="10ec8-193">hello template deploys a VM using hello VHD URI from hello earlier command.</span></span> <span data-ttu-id="10ec8-194">Distribuire il modello di hello con [distribuzione gruppo az creare](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="10ec8-194">Deploy hello template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="10ec8-195">Fornire hello URI tooyour disco rigido virtuale originale e quindi specificare il tipo di hello del sistema operativo, dimensioni della macchina virtuale e nome della macchina virtuale come segue:</span><span class="sxs-lookup"><span data-stu-id="10ec8-195">Provide hello URI tooyour original VHD and then specify hello OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="10ec8-196">Riabilitare la diagnostica di avvio</span><span class="sxs-lookup"><span data-stu-id="10ec8-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="10ec8-197">Quando si crea la macchina virtuale dal disco rigido virtuale esistente di hello, la diagnostica di avvio potrebbe non essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="10ec8-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="10ec8-198">Abilitare la diagnostica di avvio con il comando [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="10ec8-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="10ec8-199">esempio Hello consente hello un'estensione di diagnostica nella macchina virtuale denominata hello `myDeployedVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="10ec8-199">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="10ec8-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10ec8-200">Next steps</span></span>
<span data-ttu-id="10ec8-201">Se si sono verificati problemi di connessione tooyour VM, vedere [tooan connessioni risolvere SSH macchina virtuale di Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10ec8-201">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="10ec8-202">Per problemi relativi all'accesso alle applicazioni in esecuzione nella macchina virtuale, vedere [Risolvere i problemi di connettività delle applicazioni in una macchina virtuale di Azure per Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10ec8-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
