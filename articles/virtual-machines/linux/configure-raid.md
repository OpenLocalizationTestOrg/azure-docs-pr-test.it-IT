---
title: Configurare RAID software in una macchina virtuale che esegue Linux | Microsoft Docs
description: Informazioni su come usare mdadm per configurare RAID in Linux in Azure.
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
ms.openlocfilehash: 12f540a700fbf85e579e8aadc9f6def039299ff7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="d0f62-103">Configurare RAID software in Linux</span><span class="sxs-lookup"><span data-stu-id="d0f62-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="d0f62-104">I RAID software vengono spesso usati nelle macchine virtuali Linux in Azure per presentare più dischi dati collegati come se si trattasse di un singolo dispositivo RAID.</span><span class="sxs-lookup"><span data-stu-id="d0f62-104">It's a common scenario to use software RAID on Linux virtual machines in Azure to present multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="d0f62-105">In genere questa configurazione consente di migliorare le prestazioni e la velocità effettiva rispetto all'utilizzo di un unico disco.</span><span class="sxs-lookup"><span data-stu-id="d0f62-105">Typically this can be used to improve performance and allow for improved throughput compared to using just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="d0f62-106">Collegamento di dischi dati</span><span class="sxs-lookup"><span data-stu-id="d0f62-106">Attaching data disks</span></span>
<span data-ttu-id="d0f62-107">Per configurare un dispositivo RAID sono necessari due o più dischi dati vuoti.</span><span class="sxs-lookup"><span data-stu-id="d0f62-107">Two or more empty data disks are needed to configure a RAID device.</span></span>  <span data-ttu-id="d0f62-108">Il dispositivo RAID viene creato principalmente per migliorare le prestazioni dell'I/O su disco.</span><span class="sxs-lookup"><span data-stu-id="d0f62-108">The primary reason for creating a RAID device is to improve performance of your disk IO.</span></span>  <span data-ttu-id="d0f62-109">In base alle esigenze di I/O, è possibile scegliere di collegare dischi che sono archiviati nell'archiviazione Standard con un massimo di 500 IO/ps per ogni disco o nell'archiviazione Premium con un massimo di 5.000 IO/ps per ogni disco.</span><span class="sxs-lookup"><span data-stu-id="d0f62-109">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="d0f62-110">In questo articolo non verrà illustrato in dettaglio come eseguire il provisioning e collegare dischi dati a una macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="d0f62-110">This article does not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span>  <span data-ttu-id="d0f62-111">Per istruzioni dettagliate su come collegare un disco dati vuoto a una macchina virtuale Linux in Azure, vedere l'articolo di Microsoft Azure relativo al [collegamento di dischi](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0f62-111">See the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-mdadm-utility"></a><span data-ttu-id="d0f62-112">Installazione dell'utility mdadm</span><span class="sxs-lookup"><span data-stu-id="d0f62-112">Install the mdadm utility</span></span>
* <span data-ttu-id="d0f62-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="d0f62-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="d0f62-114">**CentOS e Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="d0f62-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="d0f62-115">**SLES e openSUSE**</span><span class="sxs-lookup"><span data-stu-id="d0f62-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-the-disk-partitions"></a><span data-ttu-id="d0f62-116">Creazione delle partizioni del disco</span><span class="sxs-lookup"><span data-stu-id="d0f62-116">Create the disk partitions</span></span>
<span data-ttu-id="d0f62-117">In questo esempio verrà creata una singola partizione del disco in /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="d0f62-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="d0f62-118">La nuova partizione del disco verrà denominata /dev/sdc1.</span><span class="sxs-lookup"><span data-stu-id="d0f62-118">The new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="d0f62-119">Avviare `fdisk` per iniziare la creazione delle partizioni</span><span class="sxs-lookup"><span data-stu-id="d0f62-119">Start `fdisk` to begin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide to write them.
    After that, of course, the previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off the mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="d0f62-120">Premere ' n'alla richiesta di creazione di un  **n** partizione uovo:</span><span class="sxs-lookup"><span data-stu-id="d0f62-120">Press 'n' at the prompt to create a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="d0f62-121">Successivamente, premere 'p' per creare una partizione **p**rimaria:</span><span class="sxs-lookup"><span data-stu-id="d0f62-121">Next, press 'p' to create a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="d0f62-122">Premere '1' per selezionare la partizione numero 1:</span><span class="sxs-lookup"><span data-stu-id="d0f62-122">Press '1' to select partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="d0f62-123">Selezionare il punto di inizio della nuova partizione oppure premere `<enter>` per accettare le impostazioni predefinite, che prevedono il posizionamento della partizione all'inizio dello spazio libero nell'unità:</span><span class="sxs-lookup"><span data-stu-id="d0f62-123">Select the starting point of the new partition, or press `<enter>` to accept the default to place the partition at the beginning of the free space on the drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="d0f62-124">Selezionare le dimensioni della partizione, ad esempio digitare '+10G' per creare una partizione da 10 gigabyte.</span><span class="sxs-lookup"><span data-stu-id="d0f62-124">Select the size of the partition, for example type '+10G' to create a 10 gigabyte partition.</span></span> <span data-ttu-id="d0f62-125">In alternativa, premere `<enter>` per creare un'unica partizione che occupa l'intera unità:</span><span class="sxs-lookup"><span data-stu-id="d0f62-125">Or, press `<enter>` create a single partition that spans the entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="d0f62-126">Successivamente, modificare l'ID e il **t**ipo della partizione dal valore predefinito '83' (Linux) a 'fd' (rilevamento automatico RAID Linux):</span><span class="sxs-lookup"><span data-stu-id="d0f62-126">Next, change the ID and **t**ype of the partition from the default ID '83' (Linux) to ID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L to list codes): fd
    ```

8. <span data-ttu-id="d0f62-127">Infine, scrivere la tabella delle partizioni sull'unità e chiudere fdisk:</span><span class="sxs-lookup"><span data-stu-id="d0f62-127">Finally, write the partition table to the drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    The partition table has been altered!
    ```

## <a name="create-the-raid-array"></a><span data-ttu-id="d0f62-128">Creazione dell'array RAID</span><span class="sxs-lookup"><span data-stu-id="d0f62-128">Create the RAID array</span></span>
1. <span data-ttu-id="d0f62-129">Nell'esempio seguente verrà eseguito lo striping (livello RAID 0) di tre partizioni situate in tre dischi dati separati (sdc1, sdd1, sde1).</span><span class="sxs-lookup"><span data-stu-id="d0f62-129">The following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="d0f62-130">Dopo l'esecuzione del comando verrà creato un nuovo dispositivo RAID denominato **/dev/md127** .</span><span class="sxs-lookup"><span data-stu-id="d0f62-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="d0f62-131">Si noti anche che se i dischi dati facevano precedentemente parte di una matrice RAID inattiva, può essere necessario aggiungere il parametro `--force` al comando `mdadm`:</span><span class="sxs-lookup"><span data-stu-id="d0f62-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary to add the `--force` parameter to the `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="d0f62-132">Creare il file system nel nuovo dispositivo RAID</span><span class="sxs-lookup"><span data-stu-id="d0f62-132">Create the file system on the new RAID device</span></span>
   
    <span data-ttu-id="d0f62-133">a.</span><span class="sxs-lookup"><span data-stu-id="d0f62-133">a.</span></span> <span data-ttu-id="d0f62-134">**CentOS, Oracle Linux, SLES 12, openSUSE e Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="d0f62-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="d0f62-135">b.</span><span class="sxs-lookup"><span data-stu-id="d0f62-135">b.</span></span> <span data-ttu-id="d0f62-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="d0f62-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="d0f62-137">c.</span><span class="sxs-lookup"><span data-stu-id="d0f62-137">c.</span></span> <span data-ttu-id="d0f62-138">**SLES 11**: abilitare boot.md e creare mdadm.conf</span><span class="sxs-lookup"><span data-stu-id="d0f62-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="d0f62-139">Dopo aver apportato queste modifiche nei sistemi SUSE può essere necessario il riavvio.</span><span class="sxs-lookup"><span data-stu-id="d0f62-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="d0f62-140">Questo passaggio *non* è obbligatorio su SLES 12.</span><span class="sxs-lookup"><span data-stu-id="d0f62-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="d0f62-141">Aggiungere il nuovo file a /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="d0f62-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d0f62-142">Se il file /etc/fstab non viene modificato in modo corretto, il sistema potrebbe diventare instabile.</span><span class="sxs-lookup"><span data-stu-id="d0f62-142">Improperly editing the /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="d0f62-143">In caso di dubbi, fare riferimento alla documentazione della distribuzione per informazioni su come modificare correttamente questo file.</span><span class="sxs-lookup"><span data-stu-id="d0f62-143">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="d0f62-144">È inoltre consigliabile creare una copia di backup del file /etc/fstab prima della modifica.</span><span class="sxs-lookup"><span data-stu-id="d0f62-144">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="d0f62-145">Creare il punto di montaggio desiderato per il nuovo file system, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d0f62-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="d0f62-146">Quando si modifica /etc/fstab è consigliabile utilizzare l' **UUID** anziché il nome del dispositivo per fare riferimento al file system.</span><span class="sxs-lookup"><span data-stu-id="d0f62-146">When editing /etc/fstab, the **UUID** should be used to reference the file system rather than the device name.</span></span>  <span data-ttu-id="d0f62-147">Usare l'utilità `blkid` per determinare l'UUID per il nuovo file system:</span><span class="sxs-lookup"><span data-stu-id="d0f62-147">Use the `blkid` utility to determine the UUID for the new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="d0f62-148">Aprire /etc/fstab in un editor di testo e aggiungere una voce per il nuovo file system, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d0f62-148">Open /etc/fstab in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="d0f62-149">In alternativa, in **SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="d0f62-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="d0f62-150">Salvare e chiudere /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="d0f62-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="d0f62-151">Verificare che la voce /etc/fstab sia corretta:</span><span class="sxs-lookup"><span data-stu-id="d0f62-151">Test that the /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="d0f62-152">Se questo comando genera un messaggio di errore, verificare la sintassi nel file /etc/fstab file.</span><span class="sxs-lookup"><span data-stu-id="d0f62-152">If this command results in an error message, please check the syntax in the /etc/fstab file.</span></span>
   
    <span data-ttu-id="d0f62-153">Eseguire quindi il comando `mount` per assicurarsi che il file system venga montato:</span><span class="sxs-lookup"><span data-stu-id="d0f62-153">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="d0f62-154">(Facoltativo) Parametri di avvio alternativo</span><span class="sxs-lookup"><span data-stu-id="d0f62-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="d0f62-155">**Configurazione di fstab**</span><span class="sxs-lookup"><span data-stu-id="d0f62-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="d0f62-156">Molte distribuzioni includono i parametri di montaggio `nobootwait` o `nofail`, che è possibile aggiungere al file /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="d0f62-156">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the /etc/fstab file.</span></span> <span data-ttu-id="d0f62-157">Tali parametri consentono di ignorare gli errori durante il montaggio di uno specifico file system. Consentono pertanto di proseguire l'avvio del sistema Linux anche se non è possibile montare correttamente il file system RAID.</span><span class="sxs-lookup"><span data-stu-id="d0f62-157">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="d0f62-158">Per altre informazioni su questi parametri, fare riferimento alla documentazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d0f62-158">Refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="d0f62-159">Esempio (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="d0f62-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="d0f62-160">**Parametri di avvio di Linux**</span><span class="sxs-lookup"><span data-stu-id="d0f62-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="d0f62-161">Oltre ai parametri precedenti, il parametro del kernel "`bootdegraded=true`" consente di avviare il sistema anche se il RAID viene percepito come danneggiato o con funzionalità ridotte, ad esempio se un'unità dati viene rimossa accidentalmente dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d0f62-161">In addition to the above parameters, the kernel parameter "`bootdegraded=true`" can allow the system to boot even if the RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from the virtual machine.</span></span> <span data-ttu-id="d0f62-162">Per impostazione predefinita, questa situazione può rendere impossibile l'avvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="d0f62-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="d0f62-163">Per informazioni sulla corretta modifica dei parametri del kernel, fare riferimento alla documentazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d0f62-163">Please refer to your distribution's documentation on how to properly edit kernel parameters.</span></span> <span data-ttu-id="d0f62-164">Ad esempio, in molte distribuzioni (CentOS, Oracle Linux, SLES 11) è possibile aggiungere manualmente tali parametri al file "`/boot/grub/menu.lst`".</span><span class="sxs-lookup"><span data-stu-id="d0f62-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually to the "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="d0f62-165">In Ubuntu è possibile aggiungere il parametro `GRUB_CMDLINE_LINUX_DEFAULT` alla variabile in "/etc/default/grub".</span><span class="sxs-lookup"><span data-stu-id="d0f62-165">On Ubuntu this parameter can be added to the `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="d0f62-166">Supporto per TRIM/UNMAP</span><span class="sxs-lookup"><span data-stu-id="d0f62-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="d0f62-167">Alcuni kernel di Linux supportano operazioni TRIM/UNMAP allo scopo di rimuovere i blocchi inutilizzati sul disco.</span><span class="sxs-lookup"><span data-stu-id="d0f62-167">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="d0f62-168">Nel servizio di archiviazione standard, queste operazioni sono particolarmente utili per informare Azure che le pagine eliminate non sono più valide e possono essere rimosse.</span><span class="sxs-lookup"><span data-stu-id="d0f62-168">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="d0f62-169">L'eliminazione delle pagine consente di risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="d0f62-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="d0f62-170">RAID non può inviare comandi di rimozione se le dimensioni del blocco per la matrice sono impostate su un valore inferiore a quello predefinito di 512 KB.</span><span class="sxs-lookup"><span data-stu-id="d0f62-170">RAID may not issue discard commands if the chunk size for the array is set to less than the default (512KB).</span></span> <span data-ttu-id="d0f62-171">Questo perché anche la granularità di annullamento del mapping nell'host è di 512 KB.</span><span class="sxs-lookup"><span data-stu-id="d0f62-171">This is because the unmap granularity on the Host is also 512KB.</span></span> <span data-ttu-id="d0f62-172">Se le dimensioni del blocco della matrice sono state modificate tramite il parametro `--chunk=` di mdadm, il kernel può ignorare le richieste TRIM/UNMAP.</span><span class="sxs-lookup"><span data-stu-id="d0f62-172">If you modified the array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by the kernel.</span></span>

<span data-ttu-id="d0f62-173">Esistono due modi per abilitare la funzione TRIM in una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="d0f62-173">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="d0f62-174">Come di consueto, consultare la documentazione della distribuzione per stabilire l'approccio consigliato:</span><span class="sxs-lookup"><span data-stu-id="d0f62-174">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="d0f62-175">Usare l'opzione di montaggio `discard` in `/etc/fstab`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d0f62-175">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="d0f62-176">In alcuni casi l'opzione `discard` può avere implicazioni sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d0f62-176">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="d0f62-177">In alternativa, è possibile eseguire il comando `fstrim` manualmente dalla riga di comando oppure aggiungerlo a crontab per eseguirlo a intervalli regolari:</span><span class="sxs-lookup"><span data-stu-id="d0f62-177">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="d0f62-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="d0f62-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="d0f62-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="d0f62-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
