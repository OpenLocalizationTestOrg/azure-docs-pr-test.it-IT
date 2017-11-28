---
title: Configurare LVM in una macchina virtuale che esegue Linux | Microsoft Docs
description: Informazioni su come configurare LVM su Linux in Azure.
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
ms.openlocfilehash: 7926627aaa3f0da935131f491d927ab5cb4b35c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="b22f3-103">Configurare LVM in una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="b22f3-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="b22f3-104">Questo documento illustra come configurare il gestore dei volumi logici (Logical Volume Manager, LVM) nella macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b22f3-104">This document will discuss how to configure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="b22f3-105">Sebbene sia possibile configurare una LVM su qualsiasi disco collegato alla macchina virtuale, per impostazione predefinita la maggior parte delle immagini di cloud non avrà alcuna LVM configurata sul disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="b22f3-105">While it is feasible to configure LVM on any disk attached to the virtual machine, by default most cloud images will not have LVM configured on the OS disk.</span></span> <span data-ttu-id="b22f3-106">Questa impostazione consente di evitare problemi con i gruppi di volumi duplicati se il disco del sistema operativo viene collegato a un'altra macchina virtuale dello stesso tipo e della stessa distribuzione, ad esempio durante uno scenario di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b22f3-106">This is to prevent problems with duplicate volume groups if the OS disk is ever attached to another VM of the same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="b22f3-107">Pertanto è consigliabile usare la LVM solo sui dischi dati.</span><span class="sxs-lookup"><span data-stu-id="b22f3-107">Therefore it is recommended only to use LVM on the data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="b22f3-108">Volumi lineari e volumi con striping logici</span><span class="sxs-lookup"><span data-stu-id="b22f3-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="b22f3-109">La LVM può essere usata per combinare un numero di dischi fisici in un unico volume di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b22f3-109">LVM can be used to combine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="b22f3-110">Per impostazione predefinita la LVM crea generalmente volumi logici lineari, il che significa che l'archiviazione fisica è concatenata.</span><span class="sxs-lookup"><span data-stu-id="b22f3-110">By default LVM will usually create linear logical volumes, which means that the physical storage is concatenated together.</span></span> <span data-ttu-id="b22f3-111">In questo caso, le operazioni di lettura/scrittura sono in genere inviate solo a un singolo disco.</span><span class="sxs-lookup"><span data-stu-id="b22f3-111">In this case read/write operations will typically only be sent to a single disk.</span></span> <span data-ttu-id="b22f3-112">Al contrario, è anche possibile creare volumi logici con striping in cui le operazioni di lettura e scrittura sono distribuite in più dischi contenuti nel gruppo di volumi, ad esempio simile a RAID0.</span><span class="sxs-lookup"><span data-stu-id="b22f3-112">In contrast, we can also create striped logical volumes where reads and writes are distributed to multiple disks contained in the volume group (i.e. similar to RAID0).</span></span> <span data-ttu-id="b22f3-113">Per motivi di prestazioni è probabile che si debba eseguire lo striping dei volumi logici in modo che le letture e le scritture usino tutti i dischi dati associati.</span><span class="sxs-lookup"><span data-stu-id="b22f3-113">For performance reasons it is likely you will want to stripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="b22f3-114">In questo documento viene descritto come combinare più dischi dati in un singolo gruppo di volumi e quindi creare un volume con striping logici.</span><span class="sxs-lookup"><span data-stu-id="b22f3-114">This document will describe how to combine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="b22f3-115">I passaggi seguenti sono generalizzati per funzionare con la maggior parte delle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="b22f3-115">The steps below are somewhat generalized to work with most distributions.</span></span> <span data-ttu-id="b22f3-116">Nella maggior parte dei casi le utilità e i flussi di lavoro per la gestione di LVM in Azure non sono fondamentalmente diversi da altri ambienti.</span><span class="sxs-lookup"><span data-stu-id="b22f3-116">In most cases the utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="b22f3-117">Come sempre, consultare anche il fornitore Linux per la documentazione e le procedure consigliate per l'uso delle LVM con una distribuzione particolare.</span><span class="sxs-lookup"><span data-stu-id="b22f3-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="b22f3-118">Collegamento di dischi dati</span><span class="sxs-lookup"><span data-stu-id="b22f3-118">Attaching data disks</span></span>
<span data-ttu-id="b22f3-119">In genere si preferisce iniziare con due o più dischi dati vuoti quando si usano le LVM.</span><span class="sxs-lookup"><span data-stu-id="b22f3-119">One will usually want to start with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="b22f3-120">In base alle esigenze di I/O, è possibile scegliere di collegare dischi che sono archiviati nell'archiviazione Standard con un massimo di 500 IO/ps per ogni disco o nell'archiviazione Premium con un massimo di 5.000 IO/ps per ogni disco.</span><span class="sxs-lookup"><span data-stu-id="b22f3-120">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="b22f3-121">In questo articolo non verrà illustrato in dettaglio come eseguire il provisioning e collegare dischi dati a una macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="b22f3-121">This article will not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span> <span data-ttu-id="b22f3-122">Per istruzioni dettagliate su come collegare un disco dati vuoto a una macchina virtuale Linux in Azure, vedere l'articolo di Microsoft Azure relativo al [collegamento di dischi](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b22f3-122">Please see the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-lvm-utilities"></a><span data-ttu-id="b22f3-123">Installare le utilità della LVM</span><span class="sxs-lookup"><span data-stu-id="b22f3-123">Install the LVM utilities</span></span>
* <span data-ttu-id="b22f3-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="b22f3-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="b22f3-125">**RHEL, CentOS e Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="b22f3-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="b22f3-126">**SLES 12 e openSUSE**</span><span class="sxs-lookup"><span data-stu-id="b22f3-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="b22f3-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="b22f3-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="b22f3-128">In SLES11 è anche necessario modificare `/etc/sysconfig/lvm` e impostare `LVM_ACTIVATED_ON_DISCOVERED` su "attivo":</span><span class="sxs-lookup"><span data-stu-id="b22f3-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` to "enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="b22f3-129">Configurare la LVM</span><span class="sxs-lookup"><span data-stu-id="b22f3-129">Configure LVM</span></span>
<span data-ttu-id="b22f3-130">In questa guida si presuppone che siano stati connessi tre dischi dati, che vengono indicati come `/dev/sdc`, `/dev/sdd` e `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="b22f3-130">In this guide we will assume you have attached three data disks, which we'll refer to as `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="b22f3-131">Si noti che questi nomi di percorso potrebbero non essere sempre gli stessi nella VM.</span><span class="sxs-lookup"><span data-stu-id="b22f3-131">Note that these may not always be the same path names in your VM.</span></span> <span data-ttu-id="b22f3-132">È possibile eseguire`sudo fdisk -l`o un comando simile per elencare i dischi disponibili.</span><span class="sxs-lookup"><span data-stu-id="b22f3-132">You can run '`sudo fdisk -l`' or similar command to list your available disks.</span></span>

1. <span data-ttu-id="b22f3-133">Preparare i volumi fisici:</span><span class="sxs-lookup"><span data-stu-id="b22f3-133">Prepare the physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="b22f3-134">Creare un gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="b22f3-134">Create a volume group.</span></span> <span data-ttu-id="b22f3-135">In questo esempio il nome del gruppo di volumi è `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="b22f3-135">In this example we are calling the volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="b22f3-136">Creare i volumi logici.</span><span class="sxs-lookup"><span data-stu-id="b22f3-136">Create the logical volume(s).</span></span> <span data-ttu-id="b22f3-137">Con il comando seguente si crea un singolo volume logico denominato `data-lv01` da estendere nell'intero gruppo, ma si noti che è anche possibile creare più volumi logici nel gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="b22f3-137">The command below we will create a single logical volume called `data-lv01` to span the entire volume group, but note that it is also feasible to create multiple logical volumes in the volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="b22f3-138">Formattare il volume logico</span><span class="sxs-lookup"><span data-stu-id="b22f3-138">Format the logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="b22f3-139">Con l'uso di SLES11 `-t ext3` al posto di ext4.</span><span class="sxs-lookup"><span data-stu-id="b22f3-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="b22f3-140">SLES11 supporta l'accesso in sola lettura per i file system ext4.</span><span class="sxs-lookup"><span data-stu-id="b22f3-140">SLES11 only supports read-only access to ext4 filesystems.</span></span>

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="b22f3-141">Aggiungere il nuovo file a /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="b22f3-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b22f3-142">Se il file `/etc/fstab` non viene modificato in modo corretto, il sistema potrebbe non essere disponibile per l'avvio.</span><span class="sxs-lookup"><span data-stu-id="b22f3-142">Improperly editing the `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="b22f3-143">In caso di dubbi, fare riferimento alla documentazione della distribuzione per informazioni su come modificare correttamente questo file.</span><span class="sxs-lookup"><span data-stu-id="b22f3-143">If unsure, please refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="b22f3-144">È inoltre consigliabile creare una copia di backup del file `/etc/fstab` prima della modifica.</span><span class="sxs-lookup"><span data-stu-id="b22f3-144">It is also recommended that a backup of the `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="b22f3-145">Creare il punto di montaggio desiderato per il nuovo file system, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b22f3-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="b22f3-146">Individuare il percorso del volume logico</span><span class="sxs-lookup"><span data-stu-id="b22f3-146">Locate the logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="b22f3-147">Aprire `/etc/fstab` in un editor di testo e aggiungere una voce per il nuovo file system, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b22f3-147">Open `/etc/fstab` in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="b22f3-148">Salvare e chiudere `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="b22f3-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="b22f3-149">Verificare che la voce `/etc/fstab` sia corretta:</span><span class="sxs-lookup"><span data-stu-id="b22f3-149">Test that the `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="b22f3-150">Se questo comando genera un messaggio di errore, verificare la sintassi nel file `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="b22f3-150">If this command results in an error message please check the syntax in the `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="b22f3-151">Eseguire quindi il comando `mount` per assicurarsi che il file system venga montato:</span><span class="sxs-lookup"><span data-stu-id="b22f3-151">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="b22f3-152">(Facoltativo) Parametri di avvio alternativo in `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="b22f3-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="b22f3-153">Molte distribuzioni includono i parametri di montaggio `nobootwait` o `nofail`, che è possibile aggiungere al file `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="b22f3-153">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the `/etc/fstab` file.</span></span> <span data-ttu-id="b22f3-154">Tali parametri consentono di ignorare gli errori durante il montaggio di uno specifico file system. Consentono pertanto di proseguire l'avvio del sistema Linux anche se non è possibile montare correttamente il file system RAID.</span><span class="sxs-lookup"><span data-stu-id="b22f3-154">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="b22f3-155">Per ulteriori informazioni su questi parametri, fare riferimento alla documentazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b22f3-155">Please refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="b22f3-156">Esempio (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="b22f3-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="b22f3-157">Supporto per TRIM/UNMAP</span><span class="sxs-lookup"><span data-stu-id="b22f3-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="b22f3-158">Alcuni kernel di Linux supportano operazioni TRIM/UNMAP allo scopo di rimuovere i blocchi inutilizzati sul disco.</span><span class="sxs-lookup"><span data-stu-id="b22f3-158">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="b22f3-159">Nel servizio di archiviazione standard, queste operazioni sono particolarmente utili per informare Azure che le pagine eliminate non sono più valide e possono essere rimosse.</span><span class="sxs-lookup"><span data-stu-id="b22f3-159">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="b22f3-160">L'eliminazione delle pagine consente di risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="b22f3-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="b22f3-161">Esistono due modi per abilitare la funzione TRIM in una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="b22f3-161">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="b22f3-162">Come di consueto, consultare la documentazione della distribuzione per stabilire l'approccio consigliato:</span><span class="sxs-lookup"><span data-stu-id="b22f3-162">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="b22f3-163">Usare l'opzione di montaggio `discard` in `/etc/fstab`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b22f3-163">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="b22f3-164">In alcuni casi l'opzione `discard` può avere implicazioni sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b22f3-164">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="b22f3-165">In alternativa, è possibile eseguire il comando `fstrim` manualmente dalla riga di comando oppure aggiungerlo a crontab per eseguirlo a intervalli regolari:</span><span class="sxs-lookup"><span data-stu-id="b22f3-165">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="b22f3-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="b22f3-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="b22f3-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="b22f3-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
