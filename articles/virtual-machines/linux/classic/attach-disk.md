---
title: Collegare un disco a una macchina virtuale Linux in Azure| Documentazione Microsoft
description: "Informazioni su come collegare un disco dati a una VM Linux usando il modello di distribuzione classica e inizializzare il disco affinché sia pronto per l'uso"
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
ms.openlocfilehash: 017ba7197e11c2b222082833d5acabb9e542b762
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-virtual-machine"></a><span data-ttu-id="59d0b-103">Come collegare un disco dati a una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="59d0b-103">How to Attach a Data Disk to a Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="59d0b-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="59d0b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="59d0b-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="59d0b-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="59d0b-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="59d0b-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="59d0b-107">Vedere come [collegare un disco dati tramite il modello di distribuzione di Resource Manager](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="59d0b-107">See how to [attach a data disk using the Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="59d0b-108">È possibile collegare sia dischi vuoti sia dischi contenenti dati alle VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="59d0b-108">You can attach both empty disks and disks that contain data to your Azure VMs.</span></span> <span data-ttu-id="59d0b-109">In entrambi i casi i dischi sono file con estensione vhd che risiedono in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="59d0b-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="59d0b-110">Come con l'aggiunta di un disco a un computer Linux, dopo aver collegato il disco, è necessario inizializzarlo e formattarlo affinché sia pronto per l'uso.</span><span class="sxs-lookup"><span data-stu-id="59d0b-110">As with adding any disk to a Linux machine, after you attach the disk you need to initialize and format it so it's ready for use.</span></span> <span data-ttu-id="59d0b-111">Questo articolo illustra in dettaglio come collegare sia i dischi vuoti sia i dischi contenenti dati alle VM e come inizializzare e formattare successivamente un nuovo disco.</span><span class="sxs-lookup"><span data-stu-id="59d0b-111">This article details attaching both empty disks and disks already containing data to your VMs, as well as how to then initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="59d0b-112">È consigliabile usare uno o più dischi separati per archiviare i dati di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="59d0b-112">It's a best practice to use one or more separate disks to store a virtual machine's data.</span></span> <span data-ttu-id="59d0b-113">Al momento della creazione, una macchina virtuale di Azure dispone di un disco del sistema operativo e di un disco temporaneo.</span><span class="sxs-lookup"><span data-stu-id="59d0b-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="59d0b-114">**Non usare il disco temporaneo per archiviare i dati persistenti.**</span><span class="sxs-lookup"><span data-stu-id="59d0b-114">**Do not use the temporary disk to store persistent data.**</span></span> <span data-ttu-id="59d0b-115">Come si può dedurre dal nome, fornisce solo archiviazione temporanea.</span><span class="sxs-lookup"><span data-stu-id="59d0b-115">As the name implies, it provides temporary storage only.</span></span> <span data-ttu-id="59d0b-116">Non offre funzionalità di ridondanza o backup perché non risiede nel servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="59d0b-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="59d0b-117">Il disco temporaneo è in genere gestito dall'agente Linux di Azure e viene montato automaticamente in **/mnt/resource** oppure in **/mnt** nelle immagini Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="59d0b-117">The temporary disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="59d0b-118">D'altra parte, il kernel potrebbe assegnare a un disco dati il nome `/dev/sdc`; in tal caso è necessario suddividere in partizioni, formattare e montare tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="59d0b-118">On the other hand, a data disk might be named by the Linux kernel something like `/dev/sdc`, and you need to partition, format, and mount this resource.</span></span> <span data-ttu-id="59d0b-119">Per dettagli, vedere [Guida dell'utente dell'agente Linux di Azure][Agent].</span><span class="sxs-lookup"><span data-stu-id="59d0b-119">See the [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="59d0b-120">Inizializzare un nuovo disco dati in Linux</span><span class="sxs-lookup"><span data-stu-id="59d0b-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="59d0b-121">Stabilire una connessione SSH alla VM.</span><span class="sxs-lookup"><span data-stu-id="59d0b-121">SSH to your VM.</span></span> <span data-ttu-id="59d0b-122">Per altre informazioni, vedere [Come accedere a una macchina virtuale che esegue Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="59d0b-122">For more information, see [How to log on to a virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="59d0b-123">In seguito è necessario trovare l'identificatore del dispositivo per inizializzare il disco dati.</span><span class="sxs-lookup"><span data-stu-id="59d0b-123">Next you need to find the device identifier for the data disk to initialize.</span></span> <span data-ttu-id="59d0b-124">A questo scopo è possibile procedere in due modi:</span><span class="sxs-lookup"><span data-stu-id="59d0b-124">There are two ways to do that:</span></span>
   
    <span data-ttu-id="59d0b-125">a) Grep per dispositivi SCSI nei log, come nel comando seguente:</span><span class="sxs-lookup"><span data-stu-id="59d0b-125">a) Grep for SCSI devices in the logs, such as in the following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="59d0b-126">Per le distribuzioni recenti di Ubuntu, può essere necessario usare `sudo grep SCSI /var/log/syslog` perché la registrazione in `/var/log/messages` potrebbe essere disattivata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="59d0b-126">For recent Ubuntu distributions, you may need to use `sudo grep SCSI /var/log/syslog` because logging to `/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="59d0b-127">L'identificatore dell'ultimo disco dati aggiunto verrà indicato nei messaggi visualizzati.</span><span class="sxs-lookup"><span data-stu-id="59d0b-127">You can find the identifier of the last data disk that was added in the messages that are displayed.</span></span>
   
    ![Visualizzare i messaggi relativi al disco](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="59d0b-129">OPPURE</span><span class="sxs-lookup"><span data-stu-id="59d0b-129">OR</span></span>
   
    <span data-ttu-id="59d0b-130">b) Usare il comando `lsscsi` per trovare l'ID dispositivo.</span><span class="sxs-lookup"><span data-stu-id="59d0b-130">b) Use the `lsscsi` command to find out the device id.</span></span> <span data-ttu-id="59d0b-131">`lsscsi` può essere installato tramite `yum install lsscsi` (su distribuzioni basate su Red Hat) o `apt-get install lsscsi` (su distribuzioni basate su Debian).</span><span class="sxs-lookup"><span data-stu-id="59d0b-131">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="59d0b-132">È possibile trovare il disco che si sta cercando in base al relativo *LUN* o **numero di unità logica**.</span><span class="sxs-lookup"><span data-stu-id="59d0b-132">You can find the disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="59d0b-133">Ad esempio, il *LUN* per i dischi collegati può essere facilmente trovato in `azure vm disk list <virtual-machine>` come:</span><span class="sxs-lookup"><span data-stu-id="59d0b-133">For example, the *lun* for the disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="59d0b-134">L'output è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="59d0b-134">The output is similar to the following:</span></span>

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
   
    <span data-ttu-id="59d0b-135">Confrontare questi dati con l'output di `lsscsi` per la stessa macchina virtuale di esempio:</span><span class="sxs-lookup"><span data-stu-id="59d0b-135">Compare this data with the output of `lsscsi` for the same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="59d0b-136">L'ultimo numero della tupla in ogni riga è il *lun*.</span><span class="sxs-lookup"><span data-stu-id="59d0b-136">The last number in the tuple in each row is the *lun*.</span></span> <span data-ttu-id="59d0b-137">Per altre informazioni, vedere `man lsscsi` .</span><span class="sxs-lookup"><span data-stu-id="59d0b-137">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="59d0b-138">Al prompt dei comandi, digitare il comando seguente per creare un dispositivo:</span><span class="sxs-lookup"><span data-stu-id="59d0b-138">At the prompt, type the following command to create your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="59d0b-139">Quando richiesto, digitare  **n**  per creare una partizione.</span><span class="sxs-lookup"><span data-stu-id="59d0b-139">When prompted, type **n** to create a partition.</span></span>

    ![Creare un dispositivo](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="59d0b-141">Quando richiesto, digitare **p** per impostare la partizione come partizione primaria.</span><span class="sxs-lookup"><span data-stu-id="59d0b-141">When prompted, type **p** to make the partition the primary partition.</span></span> <span data-ttu-id="59d0b-142">Digitare **1** per impostarla come prima partizione, quindi premere INVIO per accettare il valore predefinito per il cilindro.</span><span class="sxs-lookup"><span data-stu-id="59d0b-142">Type **1** to make it the first partition, and then type enter to accept the default value for the cylinder.</span></span> <span data-ttu-id="59d0b-143">In alcuni sistemi, è possibile visualizzare i valori predefiniti del primo e dell'ultimo settore e non del cilindro.</span><span class="sxs-lookup"><span data-stu-id="59d0b-143">On some systems, it can show the default values of the first and the last sectors, instead of the cylinder.</span></span> <span data-ttu-id="59d0b-144">È possibile scegliere di accettare questi valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="59d0b-144">You can choose to accept these defaults.</span></span>

    ![Creare la partizione](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="59d0b-146">Digitare **p** per visualizzare i dettagli relativi al disco da suddividere in partizioni.</span><span class="sxs-lookup"><span data-stu-id="59d0b-146">Type **p** to see the details about the disk that is being partitioned.</span></span>

    ![Visualizzare le informazioni sul disco](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="59d0b-148">Digitare **w** per scrivere le impostazioni per il disco.</span><span class="sxs-lookup"><span data-stu-id="59d0b-148">Type **w** to write the settings for the disk.</span></span>

    ![Scrivere le modifiche sul disco](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="59d0b-150">È ora possibile creare il file system nella nuova partizione.</span><span class="sxs-lookup"><span data-stu-id="59d0b-150">Now you can create the file system on the new partition.</span></span> <span data-ttu-id="59d0b-151">Aggiungere il numero della partizione all'ID del dispositivo (nell'esempio seguente `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="59d0b-151">Append the partition number to the device ID (in the following example `/dev/sdc1`).</span></span> <span data-ttu-id="59d0b-152">Nell'esempio seguente viene creata una partizione ext4 in /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="59d0b-152">The following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Creare il file system](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="59d0b-154">Che i sistemi SUSE Linux Enterprise 11 supportano solo l'accesso di sola lettura ai file system ext4.</span><span class="sxs-lookup"><span data-stu-id="59d0b-154">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="59d0b-155">Per questi sistemi è consigliabile formattare il nuovo file system come ext3 anziché ext4.</span><span class="sxs-lookup"><span data-stu-id="59d0b-155">For these systems, it is recommended to format the new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="59d0b-156">Creare una directory per il montaggio del nuovo file system nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="59d0b-156">Make a directory to mount the new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="59d0b-157">È infine possibile montare l'unità, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="59d0b-157">Finally you can mount the drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="59d0b-158">Il disco dati è ora pronto per l'uso come **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="59d0b-158">The data disk is now ready to use as **/datadrive**.</span></span>
   
    ![Creare la directory e montare il disco](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="59d0b-160">Aggiungere la nuova unità a /etc/fstab:</span><span class="sxs-lookup"><span data-stu-id="59d0b-160">Add the new drive to /etc/fstab:</span></span>
   
    <span data-ttu-id="59d0b-161">Per assicurarsi che l'unità venga rimontata automaticamente dopo un riavvio, è necessario aggiungerla al file /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="59d0b-161">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="59d0b-162">È inoltre consigliabile che l'UUID (Universally Unique IDentifier) usato in /etc/fstab faccia riferimento all'unità anziché al solo nome del dispositivo, ad esempio /dev/sdc1.</span><span class="sxs-lookup"><span data-stu-id="59d0b-162">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="59d0b-163">L'utilizzo dell'UUID evita che venga montato il disco non corretto in una posizione specificata, se il sistema operativo rileva un errore del disco durante l'avvio, e l'assegnazione di tali ID dispositivo agli eventuali dischi dati rimanenti.</span><span class="sxs-lookup"><span data-stu-id="59d0b-163">Using the UUID avoids the incorrect disk being mounted to a given location if the OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="59d0b-164">Per individuare l'UUID della nuova unità, è possibile usare l'utilità **blkid** :</span><span class="sxs-lookup"><span data-stu-id="59d0b-164">To find the UUID of the new drive, you can use the **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="59d0b-165">L'output è simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="59d0b-165">The output looks similar to the following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="59d0b-166">Se il file **/etc/fstab** non viene modificato in modo corretto, il sistema potrebbe diventare non avviabile.</span><span class="sxs-lookup"><span data-stu-id="59d0b-166">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="59d0b-167">In caso di dubbi, fare riferimento alla documentazione della distribuzione per informazioni su come modificare correttamente questo file.</span><span class="sxs-lookup"><span data-stu-id="59d0b-167">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="59d0b-168">È inoltre consigliabile creare una copia di backup del file /etc/fstab prima della modifica.</span><span class="sxs-lookup"><span data-stu-id="59d0b-168">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="59d0b-169">Successivamente, aprire il file **/etc/fstab** in un editor di testo:</span><span class="sxs-lookup"><span data-stu-id="59d0b-169">Next, open the **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="59d0b-170">In questo esempio viene usato il valore UUID del nuovo dispositivo **/dev/sdc1** creato nei passaggi precedenti e il punto di montaggio **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="59d0b-170">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="59d0b-171">Alla fine del file **/etc/fstab** aggiungere la riga di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="59d0b-171">Add the following line to the end of the **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="59d0b-172">In alternativa, su sistemi basati su SUSE Linux, potrebbe essere necessario usare un formato leggermente diverso:</span><span class="sxs-lookup"><span data-stu-id="59d0b-172">Or, on systems based on SuSE Linux you may need to use a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="59d0b-173">L'opzione `nofail` garantisce che la macchina virtuale venga avviata anche se il file system è danneggiato o il disco non esiste in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="59d0b-173">The `nofail` option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="59d0b-174">Senza questa opzione potrebbero verificarsi comportamenti come quelli descritti in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/) (Impossibile eseguire una connessione SSH su VM Linux a causa di errori FSTAB).</span><span class="sxs-lookup"><span data-stu-id="59d0b-174">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="59d0b-175">Per verificare che il file system venga montato correttamente, è possibile smontarlo e rimontarlo, ad esempio</span><span class="sxs-lookup"><span data-stu-id="59d0b-175">You can now test that the file system is mounted properly by unmounting and then remounting the file system, i.e.</span></span> <span data-ttu-id="59d0b-176">usando il punto di montaggio esemplificativo `/datadrive` creato nei passaggi precedenti:</span><span class="sxs-lookup"><span data-stu-id="59d0b-176">using the example mount point `/datadrive` created in the earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="59d0b-177">Se il comando `mount` restituisce un errore, verificare che la sintassi del file /etc/fstab sia corretta.</span><span class="sxs-lookup"><span data-stu-id="59d0b-177">If the `mount` command produces an error, check the /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="59d0b-178">Anche le eventuali altre unità o partizioni dati create devono essere inserite separatamente in /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="59d0b-178">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="59d0b-179">Rendere scrivibile l'unità tramite questo comando:</span><span class="sxs-lookup"><span data-stu-id="59d0b-179">Make the drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="59d0b-180">Se si rimuove successivamente un disco dati senza modificare fstab, è possibile che si verifichi un errore di avvio della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="59d0b-180">Subsequently removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="59d0b-181">Se si tratta di un errore ricorrente, nella maggior parte delle distribuzioni sono disponibili le opzioni fstab `nofail` e/o `nobootwait`, che consentono l'avvio di un sistema anche in caso di errore di montaggio in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="59d0b-181">If this is a common occurrence, most distributions provide either the `nofail` and/or `nobootwait` fstab options that allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="59d0b-182">Per altre informazioni su questi parametri, consultare la documentazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="59d0b-182">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="59d0b-183">Supporto delle funzioni TRIM/UNMAP per Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="59d0b-183">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="59d0b-184">Alcuni kernel di Linux supportano operazioni TRIM/UNMAP allo scopo di rimuovere i blocchi inutilizzati sul disco.</span><span class="sxs-lookup"><span data-stu-id="59d0b-184">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="59d0b-185">Nel servizio di archiviazione standard, queste operazioni sono particolarmente utili per informare Azure che le pagine eliminate non sono più valide e possono essere rimosse.</span><span class="sxs-lookup"><span data-stu-id="59d0b-185">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="59d0b-186">L'eliminazione delle pagine consente di risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="59d0b-186">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="59d0b-187">Esistono due modi per abilitare la funzione TRIM in una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="59d0b-187">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="59d0b-188">Come di consueto, consultare la documentazione della distribuzione per stabilire l'approccio consigliato:</span><span class="sxs-lookup"><span data-stu-id="59d0b-188">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="59d0b-189">Usare l'opzione di montaggio `discard` in `/etc/fstab`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="59d0b-189">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="59d0b-190">In alcuni casi l'opzione `discard` può avere implicazioni sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="59d0b-190">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="59d0b-191">In alternativa, è possibile eseguire il comando `fstrim` manualmente dalla riga di comando oppure aggiungerlo a crontab per eseguirlo a intervalli regolari:</span><span class="sxs-lookup"><span data-stu-id="59d0b-191">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="59d0b-192">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="59d0b-192">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="59d0b-193">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="59d0b-193">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="59d0b-194">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="59d0b-194">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="59d0b-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="59d0b-195">Next Steps</span></span>
<span data-ttu-id="59d0b-196">Per altre informazioni sull'uso delle VM Linux, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="59d0b-196">You can read more about using your Linux VM in the following articles:</span></span>

* <span data-ttu-id="59d0b-197">[Come accedere a una macchina virtuale che esegue Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="59d0b-197">[How to log on to a virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="59d0b-198">Informazioni su come scollegare un disco da una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="59d0b-198">How to detach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="59d0b-199">Comandi dell'interfaccia della riga di comando di Azure in modalità Gestione servizi di Azure (asm)</span><span class="sxs-lookup"><span data-stu-id="59d0b-199">Using the Azure CLI with the Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="59d0b-200">Configurare RAID in una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="59d0b-200">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="59d0b-201">Configurare LVM in una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="59d0b-201">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
