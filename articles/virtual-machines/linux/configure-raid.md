---
title: software aaaConfigure RAID in una macchina virtuale che esegue Linux | Documenti Microsoft
description: Informazioni su come toouse mdadm tooconfigure RAID su Linux in Azure.
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="db22a-103">Configurare RAID software in Linux</span><span class="sxs-lookup"><span data-stu-id="db22a-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="db22a-104">Si tratta di un software di toouse uno scenario comune RAID nelle macchine virtuali Linux in Azure toopresent dati collegati più dischi come un singolo dispositivo RAID.</span><span class="sxs-lookup"><span data-stu-id="db22a-104">It's a common scenario toouse software RAID on Linux virtual machines in Azure toopresent multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="db22a-105">In genere per possa essere utilizzati tooimprove prestazioni e migliorato velocità effettiva rispetto toousing solo un singolo disco.</span><span class="sxs-lookup"><span data-stu-id="db22a-105">Typically this can be used tooimprove performance and allow for improved throughput compared toousing just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="db22a-106">Collegamento di dischi dati</span><span class="sxs-lookup"><span data-stu-id="db22a-106">Attaching data disks</span></span>
<span data-ttu-id="db22a-107">Due o più dischi dati vuoti sono necessari tooconfigure un dispositivo RAID.</span><span class="sxs-lookup"><span data-stu-id="db22a-107">Two or more empty data disks are needed tooconfigure a RAID device.</span></span>  <span data-ttu-id="db22a-108">Hello per la creazione di un dispositivo RAID viene principalmente tooimprove delle prestazioni dei / o del disco.</span><span class="sxs-lookup"><span data-stu-id="db22a-108">hello primary reason for creating a RAID device is tooimprove performance of your disk IO.</span></span>  <span data-ttu-id="db22a-109">In base alle proprie esigenze dei / o, è possibile scegliere tooattach dischi che vengono archiviati nel nostro servizio di archiviazione Standard, con backup too500 IO/ps per ogni disco o l'archiviazione Premium con backup too5000 IO/ps per ogni disco.</span><span class="sxs-lookup"><span data-stu-id="db22a-109">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="db22a-110">In questo articolo non descritte in dettaglio sul tooprovision e collegare la macchina virtuale dati dischi tooa Linux.</span><span class="sxs-lookup"><span data-stu-id="db22a-110">This article does not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span>  <span data-ttu-id="db22a-111">Vedere articolo di Microsoft Azure hello [collegare un disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per istruzioni dettagliate su come tooattach dati vuoti di un disco di macchina virtuale di Linux tooa in Azure.</span><span class="sxs-lookup"><span data-stu-id="db22a-111">See hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-mdadm-utility"></a><span data-ttu-id="db22a-112">Installare utilità mdadm hello</span><span class="sxs-lookup"><span data-stu-id="db22a-112">Install hello mdadm utility</span></span>
* <span data-ttu-id="db22a-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="db22a-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="db22a-114">**CentOS e Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="db22a-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="db22a-115">**SLES e openSUSE**</span><span class="sxs-lookup"><span data-stu-id="db22a-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a><span data-ttu-id="db22a-116">Creare partizioni del disco di hello</span><span class="sxs-lookup"><span data-stu-id="db22a-116">Create hello disk partitions</span></span>
<span data-ttu-id="db22a-117">In questo esempio verrà creata una singola partizione del disco in /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="db22a-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="db22a-118">partizione disco nuovo Hello verrà chiamato /dev/sdc1.</span><span class="sxs-lookup"><span data-stu-id="db22a-118">hello new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="db22a-119">Avviare `fdisk` toobegin la creazione di partizioni</span><span class="sxs-lookup"><span data-stu-id="db22a-119">Start `fdisk` toobegin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="db22a-120">Premere ' n'in hello prompt toocreate un  **n** partizione uovo:</span><span class="sxs-lookup"><span data-stu-id="db22a-120">Press 'n' at hello prompt toocreate a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="db22a-121">Successivamente, premere 'p' toocreate un **p**partizione primaria:</span><span class="sxs-lookup"><span data-stu-id="db22a-121">Next, press 'p' toocreate a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="db22a-122">Premere '1' numero di partizione tooselect 1:</span><span class="sxs-lookup"><span data-stu-id="db22a-122">Press '1' tooselect partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="db22a-123">Selezionare hello punto iniziale della nuova partizione hello o premere `<enter>` partizione tooaccept hello predefinita tooplace hello all'inizio di hello di spazio libero hello hello unità:</span><span class="sxs-lookup"><span data-stu-id="db22a-123">Select hello starting point of hello new partition, or press `<enter>` tooaccept hello default tooplace hello partition at hello beginning of hello free space on hello drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="db22a-124">Selezionare dimensione hello della partizione hello, ad esempio '+10G' di tipo toocreate una partizione di 10 GB.</span><span class="sxs-lookup"><span data-stu-id="db22a-124">Select hello size of hello partition, for example type '+10G' toocreate a 10 gigabyte partition.</span></span> <span data-ttu-id="db22a-125">In alternativa, premere `<enter>` creare una singola partizione che si estende su intera unità hello:</span><span class="sxs-lookup"><span data-stu-id="db22a-125">Or, press `<enter>` create a single partition that spans hello entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="db22a-126">Successivamente, cambiare ID hello e **t**ipo di partizione hello da predefinito hello ID tooID (Linux) '83' 'fd' (auto raid Linux):</span><span class="sxs-lookup"><span data-stu-id="db22a-126">Next, change hello ID and **t**ype of hello partition from hello default ID '83' (Linux) tooID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. <span data-ttu-id="db22a-127">Infine, scrivere unità toohello tabella di partizione hello e uscire da fdisk:</span><span class="sxs-lookup"><span data-stu-id="db22a-127">Finally, write hello partition table toohello drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a><span data-ttu-id="db22a-128">Creare una matrice RAID hello</span><span class="sxs-lookup"><span data-stu-id="db22a-128">Create hello RAID array</span></span>
1. <span data-ttu-id="db22a-129">Hello seguente verrà riportato "stripe" (livello RAID 0) e tre le partizioni si trovano su tre dischi dati separati (sdc1, sdd1, sde1).</span><span class="sxs-lookup"><span data-stu-id="db22a-129">hello following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="db22a-130">Dopo l'esecuzione del comando verrà creato un nuovo dispositivo RAID denominato **/dev/md127** .</span><span class="sxs-lookup"><span data-stu-id="db22a-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="db22a-131">Si noti inoltre che se questi dati dischi è già parte di un'altra matrice RAID inattiva potrebbe essere necessario tooadd hello `--force` parametro toohello `mdadm` comando:</span><span class="sxs-lookup"><span data-stu-id="db22a-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary tooadd hello `--force` parameter toohello `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="db22a-132">Creare hello file system sul dispositivo RAID nuovo hello</span><span class="sxs-lookup"><span data-stu-id="db22a-132">Create hello file system on hello new RAID device</span></span>
   
    <span data-ttu-id="db22a-133">a.</span><span class="sxs-lookup"><span data-stu-id="db22a-133">a.</span></span> <span data-ttu-id="db22a-134">**CentOS, Oracle Linux, SLES 12, openSUSE e Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="db22a-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="db22a-135">b.</span><span class="sxs-lookup"><span data-stu-id="db22a-135">b.</span></span> <span data-ttu-id="db22a-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="db22a-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="db22a-137">c.</span><span class="sxs-lookup"><span data-stu-id="db22a-137">c.</span></span> <span data-ttu-id="db22a-138">**SLES 11**: abilitare boot.md e creare mdadm.conf</span><span class="sxs-lookup"><span data-stu-id="db22a-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="db22a-139">Dopo aver apportato queste modifiche nei sistemi SUSE può essere necessario il riavvio.</span><span class="sxs-lookup"><span data-stu-id="db22a-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="db22a-140">Questo passaggio *non* è obbligatorio su SLES 12.</span><span class="sxs-lookup"><span data-stu-id="db22a-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="db22a-141">Aggiungere hello nuovo file system troppo/ecc/fstab</span><span class="sxs-lookup"><span data-stu-id="db22a-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="db22a-142">Modifica in modo non corretto di file /etc/fstab. hello può provocare un avvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="db22a-142">Improperly editing hello /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="db22a-143">In caso di dubbi, consultare la documentazione della distribuzione toohello per informazioni su come tooproperly modificare questo file.</span><span class="sxs-lookup"><span data-stu-id="db22a-143">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="db22a-144">È inoltre consigliabile che viene creato un backup di file /etc/fstab. hello prima della modifica.</span><span class="sxs-lookup"><span data-stu-id="db22a-144">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="db22a-145">Creare il punto di montaggio hello desiderato per il nuovo file system, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="db22a-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="db22a-146">Quando si modifica /etc/fstab., hello **UUID** deve essere utilizzato tooreference hello file system anziché hello dispositivo il nome.</span><span class="sxs-lookup"><span data-stu-id="db22a-146">When editing /etc/fstab, hello **UUID** should be used tooreference hello file system rather than hello device name.</span></span>  <span data-ttu-id="db22a-147">Hello utilizzare `blkid` hello toodetermine di utilità UUID per il nuovo file system di hello:</span><span class="sxs-lookup"><span data-stu-id="db22a-147">Use hello `blkid` utility toodetermine hello UUID for hello new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="db22a-148">Aprire /etc/fstab. in un editor di testo e aggiungere una voce per hello nuovo file system, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="db22a-148">Open /etc/fstab in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="db22a-149">In alternativa, in **SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="db22a-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="db22a-150">Salvare e chiudere /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="db22a-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="db22a-151">Verificare che /etc/hosts hello/fstab voce sia corretto:</span><span class="sxs-lookup"><span data-stu-id="db22a-151">Test that hello /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="db22a-152">Se questo comando genera un messaggio di errore, controllare la sintassi di hello in file /etc/fstab. hello.</span><span class="sxs-lookup"><span data-stu-id="db22a-152">If this command results in an error message, please check hello syntax in hello /etc/fstab file.</span></span>
   
    <span data-ttu-id="db22a-153">Prossima esecuzione hello `mount` comando tooensure hello file system è montato:</span><span class="sxs-lookup"><span data-stu-id="db22a-153">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="db22a-154">(Facoltativo) Parametri di avvio alternativo</span><span class="sxs-lookup"><span data-stu-id="db22a-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="db22a-155">**Configurazione di fstab**</span><span class="sxs-lookup"><span data-stu-id="db22a-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="db22a-156">Molte distribuzioni includono entrambi hello `nobootwait` o `nofail` montare i parametri che possono essere aggiunti file di fstab toohello/e così via.</span><span class="sxs-lookup"><span data-stu-id="db22a-156">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello /etc/fstab file.</span></span> <span data-ttu-id="db22a-157">Questi parametri consentono di errori durante il montaggio di un determinato file system e consentono hello Linux sistema toocontinue tooboot anche se è Impossibile tooproperly montaggio hello RAID file sistema.</span><span class="sxs-lookup"><span data-stu-id="db22a-157">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="db22a-158">Consultare la documentazione della distribuzione tooyour per ulteriori informazioni su questi parametri.</span><span class="sxs-lookup"><span data-stu-id="db22a-158">Refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="db22a-159">Esempio (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="db22a-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="db22a-160">**Parametri di avvio di Linux**</span><span class="sxs-lookup"><span data-stu-id="db22a-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="db22a-161">In aggiunta toohello sopra i parametri, hello parametro kernel "`bootdegraded=true`" può consentire hello sistema tooboot anche se hello RAID viene considerato come danneggiato o è danneggiato, ad esempio, se un'unità dati inavvertitamente viene rimosso dalla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="db22a-161">In addition toohello above parameters, hello kernel parameter "`bootdegraded=true`" can allow hello system tooboot even if hello RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from hello virtual machine.</span></span> <span data-ttu-id="db22a-162">Per impostazione predefinita, questa situazione può rendere impossibile l'avvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="db22a-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="db22a-163">Per consultare la documentazione di tooyour della distribuzione in modalità tooproperly modificare i parametri del kernel.</span><span class="sxs-lookup"><span data-stu-id="db22a-163">Please refer tooyour distribution's documentation on how tooproperly edit kernel parameters.</span></span> <span data-ttu-id="db22a-164">Ad esempio, in molte distribuzioni (CentOS, Oracle Linux SLES 11) questi parametri possono essere aggiunti manualmente toohello "`/boot/grub/menu.lst`" file.</span><span class="sxs-lookup"><span data-stu-id="db22a-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually toohello "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="db22a-165">In Ubuntu questo parametro può essere aggiunto toohello `GRUB_CMDLINE_LINUX_DEFAULT` variabile su "/ e così via/predefinito/grub".</span><span class="sxs-lookup"><span data-stu-id="db22a-165">On Ubuntu this parameter can be added toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="db22a-166">Supporto per TRIM/UNMAP</span><span class="sxs-lookup"><span data-stu-id="db22a-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="db22a-167">Alcuni kernel Linux supporto TRIM/UNMAP operazioni toodiscard i blocchi inutilizzati nel disco hello.</span><span class="sxs-lookup"><span data-stu-id="db22a-167">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="db22a-168">Queste operazioni sono principalmente in tooinform standard di archiviazione Azure che pagine eliminate non sono più validi e possono essere ignorate.</span><span class="sxs-lookup"><span data-stu-id="db22a-168">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="db22a-169">L'eliminazione delle pagine consente di risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="db22a-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="db22a-170">RAID non può rilasciare i comandi di eliminazione se le dimensioni del blocco hello per matrice hello è impostato tooless rispetto al valore predefinito di hello (512KB).</span><span class="sxs-lookup"><span data-stu-id="db22a-170">RAID may not issue discard commands if hello chunk size for hello array is set tooless than hello default (512KB).</span></span> <span data-ttu-id="db22a-171">Infatti, annullare il mapping di hello granularità su hello Host è 512KB.</span><span class="sxs-lookup"><span data-stu-id="db22a-171">This is because hello unmap granularity on hello Host is also 512KB.</span></span> <span data-ttu-id="db22a-172">Se è stato modificato dimensioni del blocco della matrice hello tramite del mdadm `--chunk=` parametro, quindi le richieste TRIM/Annulla possono essere ignorato dal kernel hello.</span><span class="sxs-lookup"><span data-stu-id="db22a-172">If you modified hello array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by hello kernel.</span></span>

<span data-ttu-id="db22a-173">Esistono due modi tooenable TRIM supportano le VM Linux.</span><span class="sxs-lookup"><span data-stu-id="db22a-173">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="db22a-174">Come al solito, consultare la distribuzione hello approccio consigliato:</span><span class="sxs-lookup"><span data-stu-id="db22a-174">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="db22a-175">Hello utilizzare `discard` montare opzione `/etc/fstab`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="db22a-175">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="db22a-176">In alcuni hello casi `discard` opzione può avere implicazioni sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="db22a-176">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="db22a-177">In alternativa, è possibile eseguire hello `fstrim` comando manualmente dalla riga di comando hello o aggiungerlo tooyour crontab toorun regolarmente:</span><span class="sxs-lookup"><span data-stu-id="db22a-177">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="db22a-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="db22a-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="db22a-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="db22a-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
