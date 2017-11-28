---
title: aaaAttach tooa un disco VM Linux di Azure | Documenti Microsoft
description: "Informazioni su come tooattach dati disco tooa VM Linux utilizzando la distribuzione classica hello del modello e inizializzare il disco hello in modo che è pronto per l'utilizzo"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a><span data-ttu-id="b0b7a-103">Come tooAttach tooa un disco dati macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="b0b7a-103">How tooAttach a Data Disk tooa Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="b0b7a-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b0b7a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b0b7a-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b0b7a-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b0b7a-107">Vedere come troppo[collegare un disco dati con modello di distribuzione di gestione risorse di hello](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0b7a-107">See how too[attach a data disk using hello Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b0b7a-108">È possibile collegare i dischi vuoti e i dischi che contengono dati tooyour macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-108">You can attach both empty disks and disks that contain data tooyour Azure VMs.</span></span> <span data-ttu-id="b0b7a-109">In entrambi i casi i dischi sono file con estensione vhd che risiedono in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="b0b7a-110">Come con l'aggiunta di computer Linux tooa disco, dopo aver collegato il disco di hello è necessario tooinitialize e formattarlo è quindi pronto per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-110">As with adding any disk tooa Linux machine, after you attach hello disk you need tooinitialize and format it so it's ready for use.</span></span> <span data-ttu-id="b0b7a-111">Questo articolo presenta il collegamento sia i dischi vuoti e i dischi che contiene già dati tooyour le macchine virtuali, nonché come toothen inizializzare e formattare un disco nuovo.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-111">This article details attaching both empty disks and disks already containing data tooyour VMs, as well as how toothen initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="b0b7a-112">Si tratta di un migliore toouse pratica uno o più separare toostore dischi dati di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-112">It's a best practice toouse one or more separate disks toostore a virtual machine's data.</span></span> <span data-ttu-id="b0b7a-113">Al momento della creazione, una macchina virtuale di Azure dispone di un disco del sistema operativo e di un disco temporaneo.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="b0b7a-114">**Non utilizzare dati persistenti toostore di hello disco temporaneo.**</span><span class="sxs-lookup"><span data-stu-id="b0b7a-114">**Do not use hello temporary disk toostore persistent data.**</span></span> <span data-ttu-id="b0b7a-115">Come suggerisce il nome di hello, fornisce esclusivamente all'archiviazione temporanea.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-115">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="b0b7a-116">Non offre funzionalità di ridondanza o backup perché non risiede nel servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="b0b7a-117">in genere gestito da agente Linux di Azure hello e montato automaticamente troppo disco temporaneo Hello**/mnt/Retention/ risorse** (o **/mnt** sulle immagini Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="b0b7a-117">hello temporary disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="b0b7a-118">In hello invece, un disco dati potrebbe essere denominato dal kernel Linux hello simile `/dev/sdc`, ed è necessario toopartition, formattare e montare questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-118">On hello other hand, a data disk might be named by hello Linux kernel something like `/dev/sdc`, and you need toopartition, format, and mount this resource.</span></span> <span data-ttu-id="b0b7a-119">Vedere hello [Guida dell'utente dell'agente Linux Azure] [ Agent] per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-119">See hello [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="b0b7a-120">Inizializzare un nuovo disco dati in Linux</span><span class="sxs-lookup"><span data-stu-id="b0b7a-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="b0b7a-121">SSH tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-121">SSH tooyour VM.</span></span> <span data-ttu-id="b0b7a-122">Per ulteriori informazioni, vedere [come toolog nella macchina virtuale tooa che eseguono Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="b0b7a-122">For more information, see [How toolog on tooa virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="b0b7a-123">Successivamente sarà necessario identificatore del dispositivo hello toofind per hello dati disco tooinitialize.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-123">Next you need toofind hello device identifier for hello data disk tooinitialize.</span></span> <span data-ttu-id="b0b7a-124">Esistono due modi toodo che:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-124">There are two ways toodo that:</span></span>
   
    <span data-ttu-id="b0b7a-125">) Grep per i dispositivi SCSI in hello accede, ad esempio hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-125">a) Grep for SCSI devices in hello logs, such as in hello following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="b0b7a-126">Per le distribuzioni di Ubuntu recenti, potrebbe essere necessario toouse `sudo grep SCSI /var/log/syslog` perché troppo registrazione`/var/log/messages` potrebbero essere disabilitate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-126">For recent Ubuntu distributions, you may need toouse `sudo grep SCSI /var/log/syslog` because logging too`/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="b0b7a-127">È possibile trovare l'identificatore hello di hello ultimo disco dati in cui è stato aggiunto in messaggi hello che vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-127">You can find hello identifier of hello last data disk that was added in hello messages that are displayed.</span></span>
   
    ![Ottenere i messaggi hello del disco](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="b0b7a-129">OPPURE</span><span class="sxs-lookup"><span data-stu-id="b0b7a-129">OR</span></span>
   
    <span data-ttu-id="b0b7a-130">b) hello utilizzare `lsscsi` toofind comando out id dispositivo hello. `lsscsi` può essere installato mediante `yum install lsscsi` (in Red Hat in distribuzioni di base) o `apt-get install lsscsi` (in Debian in distribuzioni di base).</span><span class="sxs-lookup"><span data-stu-id="b0b7a-130">b) Use hello `lsscsi` command toofind out hello device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="b0b7a-131">È possibile trovare il disco hello desiderata dal relativo *lun* o **numero di unità logica**.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-131">You can find hello disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="b0b7a-132">Ad esempio, hello *lun* per dischi hello allegato possono essere facilmente visualizzati dal `azure vm disk list <virtual-machine>` come:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-132">For example, hello *lun* for hello disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="b0b7a-133">output di Hello è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-133">hello output is similar toohello following:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    <span data-ttu-id="b0b7a-134">Confrontare questi dati con output di hello di `lsscsi` per hello stessa macchina virtuale di esempio:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-134">Compare this data with hello output of `lsscsi` for hello same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="b0b7a-135">ultimo numero di Hello nella tupla hello in ogni riga è hello *lun*.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-135">hello last number in hello tuple in each row is hello *lun*.</span></span> <span data-ttu-id="b0b7a-136">Per altre informazioni, vedere `man lsscsi` .</span><span class="sxs-lookup"><span data-stu-id="b0b7a-136">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="b0b7a-137">Al prompt dei comandi hello, tipo hello comando che segue toocreate il dispositivo:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-137">At hello prompt, type hello following command toocreate your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="b0b7a-138">Quando richiesto, digitare  **n**  toocreate una partizione.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-138">When prompted, type **n** toocreate a partition.</span></span>

    ![Creare un dispositivo](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="b0b7a-140">Quando richiesto, digitare **p** toomake hello hello primario partizione.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-140">When prompted, type **p** toomake hello partition hello primary partition.</span></span> <span data-ttu-id="b0b7a-141">Tipo **1** toomake hello prima partizione e quindi digitare Immettere valore predefinito di hello tooaccept per cilindro hello.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-141">Type **1** toomake it hello first partition, and then type enter tooaccept hello default value for hello cylinder.</span></span> <span data-ttu-id="b0b7a-142">In alcuni sistemi può Mostra i valori predefiniti di hello di hello prima e ultima settori, anziché cilindro hello hello.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-142">On some systems, it can show hello default values of hello first and hello last sectors, instead of hello cylinder.</span></span> <span data-ttu-id="b0b7a-143">È possibile scegliere tooaccept queste impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-143">You can choose tooaccept these defaults.</span></span>

    ![Creare la partizione](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="b0b7a-145">Tipo **p** dettagli hello toosee sul disco hello viene partizionato.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-145">Type **p** toosee hello details about hello disk that is being partitioned.</span></span>

    ![Visualizzare le informazioni sul disco](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="b0b7a-147">Tipo **w** impostazioni hello toowrite per disco hello.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-147">Type **w** toowrite hello settings for hello disk.</span></span>

    ![Scrivere le modifiche ai dischi hello](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="b0b7a-149">È ora possibile creare hello file system nella nuova partizione hello.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-149">Now you can create hello file system on hello new partition.</span></span> <span data-ttu-id="b0b7a-150">Aggiungere hello partizione numero ID dispositivo toohello (nell'esempio seguente hello `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="b0b7a-150">Append hello partition number toohello device ID (in hello following example `/dev/sdc1`).</span></span> <span data-ttu-id="b0b7a-151">Hello esempio seguente viene creata una partizione ext4 su /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-151">hello following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Creare il file system](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="b0b7a-153">Che i sistemi SUSE Linux Enterprise 11 supportano solo l'accesso di sola lettura ai file system ext4.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="b0b7a-154">Per questi sistemi, è consigliabile tooformat hello nuovo file system come ext3 anziché ext4.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-154">For these systems, it is recommended tooformat hello new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="b0b7a-155">Rendere un directory toomount hello nuovo file system, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-155">Make a directory toomount hello new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="b0b7a-156">È infine possibile montare unità hello, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-156">Finally you can mount hello drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="b0b7a-157">disco dati Hello è ora pronto toouse come **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-157">hello data disk is now ready toouse as **/datadrive**.</span></span>
   
    ![Crea disco di hello hello directory di montaggio](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="b0b7a-159">Aggiungere hello nuova unità troppo/ecc/fstab:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-159">Add hello new drive too/etc/fstab:</span></span>
   
    <span data-ttu-id="b0b7a-160">unità di hello tooensure viene rimontato automaticamente dopo un riavvio del sistema che deve essere aggiunto file /etc/fstab. toohello.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-160">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="b0b7a-161">Inoltre, è consigliabile che hello UUID (Universally Unique IDentifier) viene usato in unità di toohello toorefer /etc/fstab. anziché semplicemente hello nome del dispositivo (ad esempio /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="b0b7a-161">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="b0b7a-162">Utilizzo di hello UUID evita disco non corretta di hello viene montato tooa percorso specificato, se hello del sistema operativo rileva un errore del disco durante l'avvio e di eventuali dischi dati rimanenti viene quindi assegnato a quelli ID dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-162">Using hello UUID avoids hello incorrect disk being mounted tooa given location if hello OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="b0b7a-163">toofind hello UUID della nuova unità hello, è possibile usare hello **ID blocco** utilità:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-163">toofind hello UUID of hello new drive, you can use hello **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="b0b7a-164">output di Hello è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-164">hello output looks similar toohello following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="b0b7a-165">Modifica in modo non corretto di hello **/e così via/fstab** file potrebbe causare un avvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-165">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="b0b7a-166">In caso di dubbi, consultare la documentazione della distribuzione toohello per informazioni su come tooproperly modificare questo file.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-166">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="b0b7a-167">È inoltre consigliabile che viene creato un backup di file /etc/fstab. hello prima della modifica.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-167">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="b0b7a-168">Aprire quindi hello **/e così via/fstab** file in un editor di testo:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-168">Next, open hello **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="b0b7a-169">In questo esempio, si utilizza hello UUID valore per hello nuovo **dev/sdc1** dispositivo che è stato creato in precedenza hello e punto di montaggio hello **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-169">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="b0b7a-170">Aggiungere hello successivo toohello riga alla fine di hello **/e così via/fstab** file:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-170">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="b0b7a-171">In alternativa, potrebbe essere necessario toouse un formato leggermente diverso in sistemi basati su SuSE Linux:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-171">Or, on systems based on SuSE Linux you may need toouse a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="b0b7a-172">Hello `nofail` opzione assicura che hello VM viene avviata anche se filesystem hello è danneggiato o hello disco non esiste in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-172">hello `nofail` option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="b0b7a-173">Senza questa opzione, si verifichino comportamento come descritto in [Impossibile SSH tooLinux VM a causa di errori tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span><span class="sxs-lookup"><span data-stu-id="b0b7a-173">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="b0b7a-174">È ora possibile verificare che sia installato il sistema di file hello correttamente smontare e rimontare quindi sistema file hello, ad esempio mediante punto di montaggio di esempio hello `/datadrive` creato in hello precedenti passaggi:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-174">You can now test that hello file system is mounted properly by unmounting and then remounting hello file system, i.e. using hello example mount point `/datadrive` created in hello earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="b0b7a-175">Se hello `mount` comando genera un errore, controllare hello e così via/fstab file per la sintassi corretta.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-175">If hello `mount` command produces an error, check hello /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="b0b7a-176">Anche le eventuali altre unità o partizioni dati create devono essere inserite separatamente in /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="b0b7a-177">Rendere modificabile unità hello tramite questo comando:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-177">Make hello drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="b0b7a-178">Rimozione di un disco dati successivamente senza dover modificare fstab potrebbe causare hello VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-178">Subsequently removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="b0b7a-179">Se si tratta di un problema comune, la maggior parte delle distribuzioni forniscono entrambi hello `nofail` e/o `nobootwait` fstab opzioni che consentono un tooboot di sistema, anche se il disco di hello, toomount non riesce in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-179">If this is a common occurrence, most distributions provide either hello `nofail` and/or `nobootwait` fstab options that allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="b0b7a-180">Per altre informazioni su questi parametri, consultare la documentazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-180">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="b0b7a-181">Supporto delle funzioni TRIM/UNMAP per Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="b0b7a-181">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="b0b7a-182">Alcuni kernel Linux supporto TRIM/UNMAP operazioni toodiscard i blocchi inutilizzati nel disco hello.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-182">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="b0b7a-183">Queste operazioni sono principalmente in tooinform standard di archiviazione Azure che pagine eliminate non sono più validi e possono essere ignorate.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-183">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="b0b7a-184">L'eliminazione delle pagine consente di risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-184">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="b0b7a-185">Esistono due modi tooenable TRIM supportano le VM Linux.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-185">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="b0b7a-186">Come al solito, consultare la distribuzione hello approccio consigliato:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-186">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="b0b7a-187">Hello utilizzare `discard` montare opzione `/etc/fstab`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-187">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="b0b7a-188">In alcuni hello casi `discard` opzione può avere implicazioni sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b0b7a-188">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="b0b7a-189">In alternativa, è possibile eseguire hello `fstrim` comando manualmente dalla riga di comando hello o aggiungerlo tooyour crontab toorun regolarmente:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-189">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="b0b7a-190">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="b0b7a-190">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="b0b7a-191">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="b0b7a-191">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="b0b7a-192">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="b0b7a-192">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="b0b7a-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0b7a-193">Next Steps</span></span>
<span data-ttu-id="b0b7a-194">È possibile leggere altre informazioni sull'utilizzo di VM Linux in hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="b0b7a-194">You can read more about using your Linux VM in hello following articles:</span></span>

* <span data-ttu-id="b0b7a-195">[Come toolog nella macchina virtuale tooa che esegue Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="b0b7a-195">[How toolog on tooa virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="b0b7a-196">Come toodetach un disco da una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="b0b7a-196">How toodetach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="b0b7a-197">Utilizzo di hello CLI di Azure con modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="b0b7a-197">Using hello Azure CLI with hello Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="b0b7a-198">Configurare RAID in una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="b0b7a-198">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="b0b7a-199">Configurare LVM in una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="b0b7a-199">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
