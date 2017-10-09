---
title: aaaConfigure LVM in una macchina virtuale che esegue Linux | Documenti Microsoft
description: Informazioni su come tooconfigure LVM su Linux in Azure.
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="0c7c6-103">Configurare LVM in una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="0c7c6-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="0c7c6-104">Questo documento verrà illustrate le modalità tooconfigure Manager di Volume logico (LVM) nella macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-104">This document will discuss how tooconfigure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="0c7c6-105">Sebbene sia possibile tooconfigure che LVM in qualsiasi disco collegato toohello macchina virtuale, per impostazione predefinita cloud la maggior parte delle immagini non avrà LVM configurato su hello disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-105">While it is feasible tooconfigure LVM on any disk attached toohello virtual machine, by default most cloud images will not have LVM configured on hello OS disk.</span></span> <span data-ttu-id="0c7c6-106">Si tratta di problemi tooprevent con gruppi di volumi duplicati se hello disco del sistema operativo è sempre collegata tooanother VM di hello stessa distribuzione e il tipo, ad esempio durante uno scenario di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-106">This is tooprevent problems with duplicate volume groups if hello OS disk is ever attached tooanother VM of hello same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="0c7c6-107">Pertanto è consigliabile solo nei dischi dati hello toouse LVM.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-107">Therefore it is recommended only toouse LVM on hello data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="0c7c6-108">Volumi lineari e volumi con striping logici</span><span class="sxs-lookup"><span data-stu-id="0c7c6-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="0c7c6-109">LVM può essere utilizzato toocombine un numero di dischi fisici in un singolo volume di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-109">LVM can be used toocombine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="0c7c6-110">Per impostazione predefinita LVM in genere creerà i volumi logici lineari, il che significa che l'archiviazione fisica hello è concatenato.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-110">By default LVM will usually create linear logical volumes, which means that hello physical storage is concatenated together.</span></span> <span data-ttu-id="0c7c6-111">In questo caso le operazioni di lettura/scrittura in genere solo riceverà tooa singolo disco.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-111">In this case read/write operations will typically only be sent tooa single disk.</span></span> <span data-ttu-id="0c7c6-112">Al contrario, è possibile creare anche i volumi con striping logici in cui le letture e scritture sono dischi toomultiple distribuita contenuti nel gruppo di volumi hello (vale a dire tooRAID0 simile).</span><span class="sxs-lookup"><span data-stu-id="0c7c6-112">In contrast, we can also create striped logical volumes where reads and writes are distributed toomultiple disks contained in hello volume group (i.e. similar tooRAID0).</span></span> <span data-ttu-id="0c7c6-113">Per motivi di prestazioni, che è probabile che si desidererà toostripe i volumi logici in modo che le letture e scritture utilizzano tutti i dischi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-113">For performance reasons it is likely you will want toostripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="0c7c6-114">Questo documento descrive come toocombine dischi di dati diversi in un singolo gruppo di volumi e quindi creare un volume logico con striping.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-114">This document will describe how toocombine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="0c7c6-115">passaggi Hello riportati di seguito sono in qualche modo generalizzato toowork con la maggior parte delle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-115">hello steps below are somewhat generalized toowork with most distributions.</span></span> <span data-ttu-id="0c7c6-116">In hello casi la maggior parte delle utilità e flussi di lavoro per la gestione LVM in Azure non sono fondamentalmente diversi da quello di altri ambienti.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-116">In most cases hello utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="0c7c6-117">Come sempre, consultare anche il fornitore Linux per la documentazione e le procedure consigliate per l'uso delle LVM con una distribuzione particolare.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="0c7c6-118">Collegamento di dischi dati</span><span class="sxs-lookup"><span data-stu-id="0c7c6-118">Attaching data disks</span></span>
<span data-ttu-id="0c7c6-119">Quando si utilizza LVM uno in genere consigliabile toostart con due o più dischi dati vuoti.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-119">One will usually want toostart with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="0c7c6-120">In base alle proprie esigenze dei / o, è possibile scegliere tooattach dischi che vengono archiviati nel nostro servizio di archiviazione Standard, con backup too500 IO/ps per ogni disco o l'archiviazione Premium con backup too5000 IO/ps per ogni disco.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-120">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="0c7c6-121">In questo articolo non entra in dettaglio sul tooprovision e collegare la macchina virtuale dati dischi tooa Linux.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-121">This article will not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span> <span data-ttu-id="0c7c6-122">Vedere articolo di Microsoft Azure hello [collegare un disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per istruzioni dettagliate su come tooattach dati vuoti di un disco di macchina virtuale di Linux tooa in Azure.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-122">Please see hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-lvm-utilities"></a><span data-ttu-id="0c7c6-123">Installare utilità LVM hello</span><span class="sxs-lookup"><span data-stu-id="0c7c6-123">Install hello LVM utilities</span></span>
* <span data-ttu-id="0c7c6-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="0c7c6-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="0c7c6-125">**RHEL, CentOS e Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="0c7c6-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="0c7c6-126">**SLES 12 e openSUSE**</span><span class="sxs-lookup"><span data-stu-id="0c7c6-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="0c7c6-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="0c7c6-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="0c7c6-128">In SLES11 è inoltre necessario modificare `/etc/sysconfig/lvm` e impostare `LVM_ACTIVATED_ON_DISCOVERED` troppo "Abilita":</span><span class="sxs-lookup"><span data-stu-id="0c7c6-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` too"enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="0c7c6-129">Configurare la LVM</span><span class="sxs-lookup"><span data-stu-id="0c7c6-129">Configure LVM</span></span>
<span data-ttu-id="0c7c6-130">In questa guida si presuppone che è stato collegato a tre dischi dati, che si farà riferimento tooas `/dev/sdc`, `/dev/sdd` e `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-130">In this guide we will assume you have attached three data disks, which we'll refer tooas `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="0c7c6-131">Si noti che questi potrebbe non essere sempre hello stessi nomi di percorso nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-131">Note that these may not always be hello same path names in your VM.</span></span> <span data-ttu-id="0c7c6-132">È possibile eseguire '`sudo fdisk -l`' simile toolist di comando o i dischi disponibili.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-132">You can run '`sudo fdisk -l`' or similar command toolist your available disks.</span></span>

1. <span data-ttu-id="0c7c6-133">Preparare volumi fisici hello:</span><span class="sxs-lookup"><span data-stu-id="0c7c6-133">Prepare hello physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="0c7c6-134">Creare un gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-134">Create a volume group.</span></span> <span data-ttu-id="0c7c6-135">In questo esempio stiamo chiamando il gruppo di volumi hello `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="0c7c6-135">In this example we are calling hello volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="0c7c6-136">Creare volumi logici hello.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-136">Create hello logical volume(s).</span></span> <span data-ttu-id="0c7c6-137">Hello comando seguente si creerà un singolo volume logico chiamato `data-lv01` intero volume di toospan hello gruppo, ma si noti che è anche possibile toocreate più volumi logici nel gruppo di volumi hello.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-137">hello command below we will create a single logical volume called `data-lv01` toospan hello entire volume group, but note that it is also feasible toocreate multiple logical volumes in hello volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="0c7c6-138">Volume logico hello di formato</span><span class="sxs-lookup"><span data-stu-id="0c7c6-138">Format hello logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="0c7c6-139">Con l'uso di SLES11 `-t ext3` al posto di ext4.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="0c7c6-140">SLES11 supporta solo i file System tooext4 di accesso in sola lettura.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-140">SLES11 only supports read-only access tooext4 filesystems.</span></span>

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="0c7c6-141">Aggiungere hello nuovo file system troppo/ecc/fstab</span><span class="sxs-lookup"><span data-stu-id="0c7c6-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0c7c6-142">Modifica in modo non corretto di hello `/etc/fstab` file potrebbe causare un avvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-142">Improperly editing hello `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="0c7c6-143">In caso di dubbi, consultare la documentazione della distribuzione toohello per informazioni su come tooproperly modificare questo file.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-143">If unsure, please refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="0c7c6-144">È inoltre consigliabile che un backup di hello `/etc/fstab` file viene creato prima della modifica.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-144">It is also recommended that a backup of hello `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="0c7c6-145">Creare il punto di montaggio hello desiderato per il nuovo file system, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0c7c6-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="0c7c6-146">Individuare il percorso di volume logico hello</span><span class="sxs-lookup"><span data-stu-id="0c7c6-146">Locate hello logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="0c7c6-147">Aprire `/etc/fstab` in un editor di testo e aggiungere una voce per hello nuovo file system, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0c7c6-147">Open `/etc/fstab` in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="0c7c6-148">Salvare e chiudere `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="0c7c6-149">Verificare che hello `/etc/fstab` voce sia corretta:</span><span class="sxs-lookup"><span data-stu-id="0c7c6-149">Test that hello `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="0c7c6-150">Se questo comando genera un messaggio di errore, controllare la sintassi di hello in hello `/etc/fstab` file.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-150">If this command results in an error message please check hello syntax in hello `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="0c7c6-151">Prossima esecuzione hello `mount` comando tooensure hello file system è montato:</span><span class="sxs-lookup"><span data-stu-id="0c7c6-151">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="0c7c6-152">(Facoltativo) Parametri di avvio alternativo in `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="0c7c6-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="0c7c6-153">Molte distribuzioni includono entrambi hello `nobootwait` o `nofail` montare i parametri che possono essere aggiunti toohello `/etc/fstab` file.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-153">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello `/etc/fstab` file.</span></span> <span data-ttu-id="0c7c6-154">Questi parametri consentono di errori durante il montaggio di un determinato file system e consentono hello Linux sistema toocontinue tooboot anche se è Impossibile tooproperly montaggio hello RAID file sistema.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-154">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="0c7c6-155">Per ulteriori informazioni su questi parametri, consultare la documentazione di tooyour della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-155">Please refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="0c7c6-156">Esempio (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="0c7c6-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="0c7c6-157">Supporto per TRIM/UNMAP</span><span class="sxs-lookup"><span data-stu-id="0c7c6-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="0c7c6-158">Alcuni kernel Linux supporto TRIM/UNMAP operazioni toodiscard i blocchi inutilizzati nel disco hello.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-158">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="0c7c6-159">Queste operazioni sono principalmente in tooinform standard di archiviazione Azure che pagine eliminate non sono più validi e possono essere ignorate.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-159">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="0c7c6-160">L'eliminazione delle pagine consente di risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="0c7c6-161">Esistono due modi tooenable TRIM supportano le VM Linux.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-161">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="0c7c6-162">Come al solito, consultare la distribuzione hello approccio consigliato:</span><span class="sxs-lookup"><span data-stu-id="0c7c6-162">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="0c7c6-163">Hello utilizzare `discard` montare opzione `/etc/fstab`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0c7c6-163">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="0c7c6-164">In alcuni hello casi `discard` opzione può avere implicazioni sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="0c7c6-164">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="0c7c6-165">In alternativa, è possibile eseguire hello `fstrim` comando manualmente dalla riga di comando hello o aggiungerlo tooyour crontab toorun regolarmente:</span><span class="sxs-lookup"><span data-stu-id="0c7c6-165">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="0c7c6-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="0c7c6-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="0c7c6-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="0c7c6-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
