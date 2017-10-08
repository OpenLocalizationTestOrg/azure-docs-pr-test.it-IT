---
title: prestazioni di MySQL in Linux aaaOptimize | Documenti Microsoft
description: Informazioni su come toooptimize MySQL in esecuzione in una macchina virtuale di Azure (VM) in esecuzione Linux.
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="43c37-103">Ottimizzare le prestazioni di MySQL in macchine virtuali Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="43c37-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="43c37-104">Esistono molti fattori che influiscono sulle prestazioni di MySQL in Azure, sia nella selezione dell'hardware virtuale sia nella configurazione software.</span><span class="sxs-lookup"><span data-stu-id="43c37-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="43c37-105">Questo articolo è incentrato sull'ottimizzazione delle prestazioni tramite la configurazione dell'archiviazione, del sistema e del database.</span><span class="sxs-lookup"><span data-stu-id="43c37-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43c37-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="43c37-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="43c37-107">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="43c37-108">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="43c37-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="43c37-109">Per informazioni sull'ottimizzazione di VM Linux con il modello di gestione risorse hello, vedere [ottimizzare le VM Linux in Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43c37-109">For information about Linux VM optimizations with hello Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="43c37-110">Usare RAID in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="43c37-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="43c37-111">L'archiviazione è fattore chiave hello che influisce sulle prestazioni di database in ambienti di cloud.</span><span class="sxs-lookup"><span data-stu-id="43c37-111">Storage is hello key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="43c37-112">Singolo disco tooa confrontati, RAID possono accedere più rapidamente tramite la concorrenza.</span><span class="sxs-lookup"><span data-stu-id="43c37-112">Compared tooa single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="43c37-113">Per altre informazioni, vedere la pagina [Livelli RAID standard](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="43c37-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="43c37-114">Tramite RAID è possibile migliorare la velocità effettiva di I/O del disco e il tempo di risposta di I/O in Azure.</span><span class="sxs-lookup"><span data-stu-id="43c37-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="43c37-115">I lab di test indicano che può raddoppiare la velocità effettiva dei / o disco e il tempo di risposta dei / o può essere ridotto metà medio quando hello numero di dischi RAID è raddoppiato (da toofour due, quattro tooeight e così via).</span><span class="sxs-lookup"><span data-stu-id="43c37-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when hello number of RAID disks is doubled (from two toofour, four tooeight, etc.).</span></span> <span data-ttu-id="43c37-116">Per informazioni dettagliate, vedere [Appendice A](#AppendixA) .</span><span class="sxs-lookup"><span data-stu-id="43c37-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="43c37-117">Inoltre i/o toodisk, le prestazioni di MySQL migliorano quando si aumenta il livello RAID hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-117">In addition toodisk I/O, MySQL performance improves when you increase hello RAID level.</span></span>  <span data-ttu-id="43c37-118">Per informazioni dettagliate, vedere [Appendice B](#AppendixB) .</span><span class="sxs-lookup"><span data-stu-id="43c37-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="43c37-119">È inoltre possibile dimensioni del blocco tooconsider hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-119">You might also want tooconsider hello chunk size.</span></span> <span data-ttu-id="43c37-120">In generale, con blocchi di dimensioni maggiori si ha un sovraccarico ridotto, soprattutto per le scritture di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="43c37-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="43c37-121">Tuttavia, quando una dimensione blocco hello è troppo grande, potrebbe aggiungere overhead aggiuntivo che consente di sfruttare i vantaggi di RAID.</span><span class="sxs-lookup"><span data-stu-id="43c37-121">However, when hello chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="43c37-122">dimensione predefinita corrente Hello è 512 KB, che viene dimostrata toobe ottimale per ambienti di produzione più generali.</span><span class="sxs-lookup"><span data-stu-id="43c37-122">hello current default size is 512 KB, which is proven toobe optimal for most general production environments.</span></span> <span data-ttu-id="43c37-123">Per informazioni dettagliate, vedere [Appendice C](#AppendixC) .</span><span class="sxs-lookup"><span data-stu-id="43c37-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="43c37-124">Esistono limiti al numero di dischi che è possibile aggiungere per i diversi tipi di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="43c37-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="43c37-125">Questi limiti sono descritti in dettaglio in [Dimensioni delle macchine virtuali e dei servizi cloud per Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="43c37-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="43c37-126">Sarà necessario quattro dati collegati dischi toofollow hello RAID riportato in questo articolo, sebbene sia possibile tooset backup RAID con un minor numero di dischi.</span><span class="sxs-lookup"><span data-stu-id="43c37-126">You will need four attached data disks toofollow hello RAID example in this article, although you can choose tooset up RAID with fewer disks.</span></span>  

<span data-ttu-id="43c37-127">In questo articolo si presuppone che l'utente abbia già creato una macchina virtuale Linux e che MYSQL sia già stato installato e configurato.</span><span class="sxs-lookup"><span data-stu-id="43c37-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="43c37-128">Per ulteriori informazioni sui concetti introduttivi, vedere come tooinstall MySQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="43c37-128">For more information on getting started, see How tooinstall MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="43c37-129">Configurare RAID in Azure</span><span class="sxs-lookup"><span data-stu-id="43c37-129">Set up RAID on Azure</span></span>
<span data-ttu-id="43c37-130">Hello passaggi seguenti mostrano come toocreate RAID in Azure utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="43c37-130">hello following steps show how toocreate RAID on Azure by using hello Azure portal.</span></span> <span data-ttu-id="43c37-131">È inoltre possibile configurare RAID usando gli script di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="43c37-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="43c37-132">In questo esempio verrà configurato RAID 0 con quattro dischi.</span><span class="sxs-lookup"><span data-stu-id="43c37-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a><span data-ttu-id="43c37-133">Aggiungere una macchina virtuale tooyour di dati su disco</span><span class="sxs-lookup"><span data-stu-id="43c37-133">Add a data disk tooyour virtual machine</span></span>
<span data-ttu-id="43c37-134">Nel portale di Azure hello, toohello dashboard scegliere hello toowhich di macchina virtuale si desidera tooadd un disco dati.</span><span class="sxs-lookup"><span data-stu-id="43c37-134">In hello Azure portal, go toohello dashboard and select hello virtual machine toowhich you want tooadd a data disk.</span></span> <span data-ttu-id="43c37-135">In questo esempio, macchina virtuale hello è mysqlnode1.</span><span class="sxs-lookup"><span data-stu-id="43c37-135">In this example, hello virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="43c37-136">Fare clic su **Dischi** e quindi su **Collega nuovo**.</span><span class="sxs-lookup"><span data-stu-id="43c37-136">Click **Disks** and then click **Attach New**.</span></span>

![Aggiunta di dischi nelle macchine virtuali](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="43c37-138">Creare un nuovo disco da 500 GB.</span><span class="sxs-lookup"><span data-stu-id="43c37-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="43c37-139">Assicurarsi che **preferenze Cache dell'Host** è troppo**Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="43c37-139">Make sure that **Host Cache Preference** is set too**None**.</span></span>  <span data-ttu-id="43c37-140">Al termine, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="43c37-140">When you're finished, click **OK**.</span></span>

![Attach Empty Disk](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="43c37-142">Verrà aggiunto un disco vuoto nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="43c37-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="43c37-143">Ripetere questo passaggio tre volte in modo da disporre di quattro dischi dati per RAID.</span><span class="sxs-lookup"><span data-stu-id="43c37-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="43c37-144">È possibile visualizzare hello aggiunto unità nella macchina virtuale di hello esaminando i log dei messaggi hello del kernel.</span><span class="sxs-lookup"><span data-stu-id="43c37-144">You can see hello added drives in hello virtual machine by looking at hello kernel message log.</span></span> <span data-ttu-id="43c37-145">Ad esempio, toosee sull'Ubuntu, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="43c37-145">For example, toosee this on Ubuntu, use hello following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a><span data-ttu-id="43c37-146">Creare RAID con hello dischi aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="43c37-146">Create RAID with hello additional disks</span></span>
<span data-ttu-id="43c37-147">Hello passaggi seguenti viene descritto come troppo[configurare software RAID su Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43c37-147">hello following steps describe how too[configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="43c37-148">Se si utilizza hello XFS file system, eseguire hello seguendo i passaggi dopo aver creato RAID.</span><span class="sxs-lookup"><span data-stu-id="43c37-148">If you are using hello XFS file system, execute hello following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="43c37-149">tooinstall XFS in Debian o Ubuntu Linux menta, hello utilizzare comando seguente:</span><span class="sxs-lookup"><span data-stu-id="43c37-149">tooinstall XFS on Debian, Ubuntu, or Linux Mint, use hello following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="43c37-150">tooinstall XFS su Fedora, CentOS o RHEL, hello utilizzare comando seguente:</span><span class="sxs-lookup"><span data-stu-id="43c37-150">tooinstall XFS on Fedora, CentOS, or RHEL, use hello following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="43c37-151">Impostare un nuovo percorso di archiviazione</span><span class="sxs-lookup"><span data-stu-id="43c37-151">Set up a new storage path</span></span>
<span data-ttu-id="43c37-152">Utilizzare hello tooset comando backup di un nuovo percorso di archiviazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="43c37-152">Use hello following command tooset up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a><span data-ttu-id="43c37-153">Copia hello dati toohello nuovo percorso di archiviazione originale</span><span class="sxs-lookup"><span data-stu-id="43c37-153">Copy hello original data toohello new storage path</span></span>
<span data-ttu-id="43c37-154">Utilizzare hello comando toocopy dati toohello nuovo percorso di archiviazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="43c37-154">Use hello following command toocopy data toohello new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a><span data-ttu-id="43c37-155">Modificare le autorizzazioni, pertanto può accedere a MySQL (lettura e scrittura) disco dati hello</span><span class="sxs-lookup"><span data-stu-id="43c37-155">Modify permissions so MySQL can access (read and write) hello data disk</span></span>
<span data-ttu-id="43c37-156">Utilizzare queste autorizzazioni toomodify comando hello:</span><span class="sxs-lookup"><span data-stu-id="43c37-156">Use hello following command toomodify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a><span data-ttu-id="43c37-157">Regolare i/o disco hello algoritmo di pianificazione</span><span class="sxs-lookup"><span data-stu-id="43c37-157">Adjust hello disk I/O scheduling algorithm</span></span>
<span data-ttu-id="43c37-158">Linux implementa quattro tipi di algoritmi di pianificazione di I/O:</span><span class="sxs-lookup"><span data-stu-id="43c37-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="43c37-159">Algoritmo NOOP (Nessuna operazione)</span><span class="sxs-lookup"><span data-stu-id="43c37-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="43c37-160">Algoritmo di scadenza (Scadenza)</span><span class="sxs-lookup"><span data-stu-id="43c37-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="43c37-161">Algoritmo di accodamento pienamente equo (CFQ, Completely fair queuing)</span><span class="sxs-lookup"><span data-stu-id="43c37-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="43c37-162">Algoritmo del periodo di budget (Anticipatorio)</span><span class="sxs-lookup"><span data-stu-id="43c37-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="43c37-163">È possibile selezionare diversi i/o le utilità di pianificazione in prestazioni toooptimize scenari diversi.</span><span class="sxs-lookup"><span data-stu-id="43c37-163">You can select different I/O schedulers under different scenarios toooptimize performance.</span></span> <span data-ttu-id="43c37-164">In un ambiente ad accesso casuale completamente, non c'è una differenza significativa tra hello CFQ e gli algoritmi di data di scadenza per le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="43c37-164">In a completely random access environment, there is not a significant difference between hello CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="43c37-165">È consigliabile impostare hello tooDeadline ambiente database di MySQL per la stabilità.</span><span class="sxs-lookup"><span data-stu-id="43c37-165">We recommend that you set hello MySQL database environment tooDeadline for stability.</span></span> <span data-ttu-id="43c37-166">Se è presente un I/O sequenziale considerevole, l'algoritmo CFQ potrebbe ridurre le prestazioni di I/O del disco.</span><span class="sxs-lookup"><span data-stu-id="43c37-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="43c37-167">Per unità SSD e altri dispositivi, è possibile ottenere prestazioni migliori rispetto a utilità di pianificazione predefinita hello NOOP o data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="43c37-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than hello default scheduler.</span></span>   

<span data-ttu-id="43c37-168">Toohello precedente kernel 2.5, i/o predefinito hello algoritmo di pianificazione è scadenza.</span><span class="sxs-lookup"><span data-stu-id="43c37-168">Prior toohello kernel 2.5, hello default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="43c37-169">A partire da kernel hello 2.6.18, CFQ è diventato algoritmo di pianificazione di hello predefinito i/o.</span><span class="sxs-lookup"><span data-stu-id="43c37-169">Starting with hello kernel 2.6.18, CFQ became hello default I/O scheduling algorithm.</span></span>  <span data-ttu-id="43c37-170">È possibile specificare questa impostazione in fase di avvio del kernel o modificare dinamicamente questa impostazione quando è in esecuzione il sistema hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-170">You can specify this setting at kernel boot time or dynamically modify this setting when hello system is running.</span></span>  

<span data-ttu-id="43c37-171">Hello di esempio seguente viene illustrato come toocheck e set hello dell'utilità di pianificazione toohello NOOP predefinito nella famiglia di distribuzione Debian hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-171">hello following example demonstrates how toocheck and set hello default scheduler toohello NOOP algorithm in hello Debian distribution family.</span></span>  

### <a name="view-hello-current-io-scheduler"></a><span data-ttu-id="43c37-172">Visualizzazione hello correnti i/o dell'utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="43c37-172">View hello current I/O scheduler</span></span>
<span data-ttu-id="43c37-173">utilità di pianificazione hello tooview eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="43c37-173">tooview hello scheduler run hello following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="43c37-174">Verrà visualizzato dopo l'output, che indica l'utilità di pianificazione corrente hello:</span><span class="sxs-lookup"><span data-stu-id="43c37-174">You will see following output, which indicates hello current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a><span data-ttu-id="43c37-175">Modifica dispositivo corrente hello (dev/sda) dell'algoritmo di pianificazione hello i/o</span><span class="sxs-lookup"><span data-stu-id="43c37-175">Change hello current device (/dev/sda) of hello I/O scheduling algorithm</span></span>
<span data-ttu-id="43c37-176">Eseguire hello dispositivo corrente di comandi toochange hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="43c37-176">Run hello following commands toochange hello current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="43c37-177">Impostare questa opzione solo per /dev/sda è inutile.</span><span class="sxs-lookup"><span data-stu-id="43c37-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="43c37-178">Deve essere impostato su tutti i dischi di dati in cui risiede il database di hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-178">It must be set on all data disks where hello database resides.</span></span>  
>
>

<span data-ttu-id="43c37-179">È necessario visualizzare hello seguendo l'output, che indica che grub.cfg è stato ricompilato correttamente e che l'utilità di pianificazione predefinita hello è stato aggiornato tooNOOP:</span><span class="sxs-lookup"><span data-stu-id="43c37-179">You should see hello following output, indicating that grub.cfg has been rebuilt successfully and that hello default scheduler has been updated tooNOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="43c37-180">Per hello famiglia distribuzione Red Hat, è necessario solo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="43c37-180">For hello Red Hat distribution family, you need only hello following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="43c37-181">Configurare le impostazioni per le operazioni del file system</span><span class="sxs-lookup"><span data-stu-id="43c37-181">Configure system file operations settings</span></span>
<span data-ttu-id="43c37-182">Una procedura consigliata è hello toodisable *per volta* funzionalità di registrazione nel file system di hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-182">One best practice is toodisable hello *atime* logging feature on hello file system.</span></span> <span data-ttu-id="43c37-183">Per volta è hello ora ultimo accesso file.</span><span class="sxs-lookup"><span data-stu-id="43c37-183">Atime is hello last file access time.</span></span> <span data-ttu-id="43c37-184">Ogni volta che si accede a un file, i record di sistema di hello file hello timestamp nel log di hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-184">Whenever a file is accessed, hello file system records hello timestamp in hello log.</span></span> <span data-ttu-id="43c37-185">Tuttavia, queste informazioni vengono usate raramente.</span><span class="sxs-lookup"><span data-stu-id="43c37-185">However, this information is rarely used.</span></span> <span data-ttu-id="43c37-186">Se non è necessaria, è possibile disabilitare questa opzione, riducendo così il tempo complessivo di accesso al disco.</span><span class="sxs-lookup"><span data-stu-id="43c37-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="43c37-187">per volta toodisable registrazione, è necessario toomodify hello file system configuration file /etc/ fstab e aggiungere hello **noatime** opzione.</span><span class="sxs-lookup"><span data-stu-id="43c37-187">toodisable atime logging, you need toomodify hello file system configuration file /etc/ fstab and add hello **noatime** option.</span></span>  

<span data-ttu-id="43c37-188">Ad esempio, modificare hello vim /etc/fstab. file aggiungendo noatime hello, come mostrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="43c37-188">For example, edit hello vim /etc/fstab file, adding hello noatime as shown in hello following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="43c37-189">Quindi, è possibile rimontare hello file system con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="43c37-189">Then, remount hello file system with hello following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="43c37-190">Hello test modificato risultato.</span><span class="sxs-lookup"><span data-stu-id="43c37-190">Test hello modified result.</span></span> <span data-ttu-id="43c37-191">Quando si modifica il file di test hello, hello ora di accesso non viene aggiornata.</span><span class="sxs-lookup"><span data-stu-id="43c37-191">When you modify hello test file, hello access time is not updated.</span></span> <span data-ttu-id="43c37-192">Hello seguenti esempi viene illustrato il codice hello aspetto prima e dopo la modifica.</span><span class="sxs-lookup"><span data-stu-id="43c37-192">hello following examples show what hello code looks like before and after modification.</span></span>

<span data-ttu-id="43c37-193">Prima:</span><span class="sxs-lookup"><span data-stu-id="43c37-193">Before:</span></span>        

![Codice prima delle modifiche di accesso][5]

<span data-ttu-id="43c37-195">Dopo:</span><span class="sxs-lookup"><span data-stu-id="43c37-195">After:</span></span>

![Codice dopo le modifiche di accesso][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="43c37-197">Aumentare hello il numero massimo di handle del sistema per la concorrenza elevata</span><span class="sxs-lookup"><span data-stu-id="43c37-197">Increase hello maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="43c37-198">MySQL è un database a concorrenza elevata.</span><span class="sxs-lookup"><span data-stu-id="43c37-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="43c37-199">numero di handle simultanei di Hello predefinito è 1024 per Linux, che non è sempre sufficiente.</span><span class="sxs-lookup"><span data-stu-id="43c37-199">hello default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="43c37-200">Utilizzare hello seguendo i passaggi tooincrease hello massimo simultanee gli handle di concorrenza elevata hello sistema toosupport di MySQL.</span><span class="sxs-lookup"><span data-stu-id="43c37-200">Use hello following steps tooincrease hello maximum concurrent handles of hello system toosupport high concurrency of MySQL.</span></span>

### <a name="modify-hello-limitsconf-file"></a><span data-ttu-id="43c37-201">Modificare il file di limits.conf hello</span><span class="sxs-lookup"><span data-stu-id="43c37-201">Modify hello limits.conf file</span></span>
<span data-ttu-id="43c37-202">hello tooincrease massimo consentiti handle simultanei, aggiungere hello seguenti quattro righe nel file /etc/security/limits.conf hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-202">tooincrease hello maximum allowed concurrent handles, add hello following four lines in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="43c37-203">Si noti che numero massimo di hello in grado di supportare sistema hello è 65536.</span><span class="sxs-lookup"><span data-stu-id="43c37-203">Note that 65536 is hello maximum number that hello system can support.</span></span>   

    * <span data-ttu-id="43c37-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="43c37-204">soft nofile 65536</span></span>
    * <span data-ttu-id="43c37-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="43c37-205">hard nofile 65536</span></span>
    * <span data-ttu-id="43c37-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="43c37-206">soft nproc 65536</span></span>
    * <span data-ttu-id="43c37-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="43c37-207">hard nproc 65536</span></span>

### <a name="update-hello-system-for-hello-new-limits"></a><span data-ttu-id="43c37-208">Aggiornare il sistema di hello nuovi limiti hello</span><span class="sxs-lookup"><span data-stu-id="43c37-208">Update hello system for hello new limits</span></span>
<span data-ttu-id="43c37-209">sistema di hello tooupdate, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="43c37-209">tooupdate hello system, run hello following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a><span data-ttu-id="43c37-210">Assicurarsi che i limiti di hello vengano aggiornati in fase di avvio</span><span class="sxs-lookup"><span data-stu-id="43c37-210">Ensure that hello limits are updated at boot time</span></span>
<span data-ttu-id="43c37-211">Inserire i seguenti comandi di avvio nel file /etc/rc.local hello in modo ha effetto in fase di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-211">Put hello following startup commands in hello /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="43c37-212">Ottimizzare il database MySQL</span><span class="sxs-lookup"><span data-stu-id="43c37-212">MySQL database optimization</span></span>
<span data-ttu-id="43c37-213">tooconfigure MySQL in Azure, è possibile utilizzare hello stessa strategia di ottimizzazione delle prestazioni si utilizza un computer locale.</span><span class="sxs-lookup"><span data-stu-id="43c37-213">tooconfigure MySQL on Azure, you can use hello same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="43c37-214">regole di ottimizzazione i/o principale Hello sono:</span><span class="sxs-lookup"><span data-stu-id="43c37-214">hello main I/O optimization rules are:</span></span>   

* <span data-ttu-id="43c37-215">Aumentare la dimensione della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-215">Increase hello cache size.</span></span>
* <span data-ttu-id="43c37-216">Ridurre il tempo di risposta di I/O.</span><span class="sxs-lookup"><span data-stu-id="43c37-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="43c37-217">impostazioni di server MySQL toooptimize, è possibile aggiornare il file my.cnf hello, ovvero file di configurazione hello predefinito per i computer client e server.</span><span class="sxs-lookup"><span data-stu-id="43c37-217">toooptimize MySQL server settings, you can update hello my.cnf file, which is hello default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="43c37-218">Hello elementi di configurazione seguenti sono i fattori principali hello che influiscono sulle prestazioni di MySQL:</span><span class="sxs-lookup"><span data-stu-id="43c37-218">hello following configuration items are hello main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="43c37-219">**innodb_buffer_pool_size**: pool di buffer hello contiene dati memorizzati nel buffer e indice hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-219">**innodb_buffer_pool_size**: hello buffer pool contains buffered data and hello index.</span></span> <span data-ttu-id="43c37-220">È in genere impostato too70 percento della memoria fisica.</span><span class="sxs-lookup"><span data-stu-id="43c37-220">This is usually set too70 percent of physical memory.</span></span>
* <span data-ttu-id="43c37-221">**innodb_log_file_size**: si tratta di dimensioni del log rollforward hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-221">**innodb_log_file_size**: This is hello redo log size.</span></span> <span data-ttu-id="43c37-222">Utilizzare tooensure i log di rollforward che le operazioni di scrittura sono veloce, affidabile e ripristinabile dopo un arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="43c37-222">You use redo logs tooensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="43c37-223">Viene impostato too512 MB, che consentono una notevole quantità di spazio per la registrazione di operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="43c37-223">This is set too512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="43c37-224">**max_connections**: in alcuni casi le applicazioni non chiudono correttamente le connessioni.</span><span class="sxs-lookup"><span data-stu-id="43c37-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="43c37-225">Un valore più grande server avrà a disposizione hello più tempo toorecycle reso inattivo connessioni.</span><span class="sxs-lookup"><span data-stu-id="43c37-225">A larger value will give hello server more time toorecycle idled connections.</span></span> <span data-ttu-id="43c37-226">Hello il numero massimo di connessioni è 10.000, ma consigliato di hello valore massimo è 5000.</span><span class="sxs-lookup"><span data-stu-id="43c37-226">hello maximum number of connections is 10,000, but hello recommended maximum is 5,000.</span></span>
* <span data-ttu-id="43c37-227">**Innodb_file_per_table**: questa impostazione Abilita o disabilita il possibilità hello InnoDB toostore tabelle in file distinti.</span><span class="sxs-lookup"><span data-stu-id="43c37-227">**Innodb_file_per_table**: This setting enables or disables hello ability of InnoDB toostore tables in separate files.</span></span> <span data-ttu-id="43c37-228">Attivare tooensure opzione hello che diverse operazioni di amministrazione avanzata possono essere applicate in modo efficiente.</span><span class="sxs-lookup"><span data-stu-id="43c37-228">Turn on hello option tooensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="43c37-229">Dal punto di vista delle prestazioni, può velocizzare la trasmissione di spazio di tabella hello e ottimizzare le prestazioni di Gestione frammenti di hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-229">From a performance point of view, it can speed up hello table space transmission and optimize hello debris management performance.</span></span> <span data-ttu-id="43c37-230">Hello consigliata l'impostazione per questa opzione è impostata su ON.</span><span class="sxs-lookup"><span data-stu-id="43c37-230">hello recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="43c37-231">Da MySQL 5.6, impostazione predefinita hello è impostata su ON, pertanto è necessaria alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="43c37-231">From MySQL 5.6, hello default setting is ON, so no action is required.</span></span> <span data-ttu-id="43c37-232">Per le versioni precedenti, impostazione predefinita hello è impostata su OFF.</span><span class="sxs-lookup"><span data-stu-id="43c37-232">For earlier versions, hello default setting is OFF.</span></span> <span data-ttu-id="43c37-233">impostazione di Hello deve essere modificate prima di caricare dati, perché sono interessate solo tabelle appena create.</span><span class="sxs-lookup"><span data-stu-id="43c37-233">hello setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="43c37-234">**innodb_flush_log_at_trx_commit**: valore predefinito di hello è 1, con hello ambito impostato too0 ~ 2.</span><span class="sxs-lookup"><span data-stu-id="43c37-234">**innodb_flush_log_at_trx_commit**: hello default value is 1, with hello scope set too0~2.</span></span> <span data-ttu-id="43c37-235">valore predefinito di Hello è hello più adatto per il database MySQL.</span><span class="sxs-lookup"><span data-stu-id="43c37-235">hello default value is hello most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="43c37-236">2 abilita l'impostazione Hello hello la maggior parte dell'integrità dei dati ed è adatto per cluster MySQL Master.</span><span class="sxs-lookup"><span data-stu-id="43c37-236">hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="43c37-237">impostazione di Hello pari a 0 consente la perdita di dati, che può influenzare l'affidabilità (in alcuni casi con prestazioni migliori) ed è adatto per l'istanza Slave in MySQL Cluster.</span><span class="sxs-lookup"><span data-stu-id="43c37-237">hello setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="43c37-238">**Innodb_log_buffer_size**: buffer del log hello consente transazioni toorun senza tooflush hello log toodisk prima del commit di transazioni hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-238">**Innodb_log_buffer_size**: hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit.</span></span> <span data-ttu-id="43c37-239">Tuttavia, se è presente il campo di testo o oggetto binario di grandi dimensioni, verranno utilizzate le cache di hello rapidamente e i/o disco frequenti verrà attivato.</span><span class="sxs-lookup"><span data-stu-id="43c37-239">However, if there is large binary object or text field, hello cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="43c37-240">È meglio aumentare la dimensione del buffer hello se la variabile di stato Innodb_log_waits non è 0.</span><span class="sxs-lookup"><span data-stu-id="43c37-240">It is better increase hello buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="43c37-241">**query_cache_size**: opzione migliore hello è toodisable dall'inizio hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-241">**query_cache_size**: hello best option is toodisable it from hello outset.</span></span> <span data-ttu-id="43c37-242">Impostare too0 query_cache_size (si tratta di impostazione hello di MySQL 5.6) e utilizzare altri metodi toospeed delle query.</span><span class="sxs-lookup"><span data-stu-id="43c37-242">Set query_cache_size too0 (this is hello default setting in MySQL 5.6) and use other methods toospeed up queries.</span></span>  

<span data-ttu-id="43c37-243">Vedere [appendice D](#AppendixD) per un confronto tra le prestazioni prima e dopo l'ottimizzazione di hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-243">See [Appendix D](#AppendixD) for a comparison of performance before and after hello optimization.</span></span>

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a><span data-ttu-id="43c37-244">Attivare i log di query lente hello MySQL per l'analisi dei colli di bottiglia delle prestazioni hello</span><span class="sxs-lookup"><span data-stu-id="43c37-244">Turn on hello MySQL slow query log for analyzing hello performance bottleneck</span></span>
<span data-ttu-id="43c37-245">log query lente di MySQL Hello consentono di identificare query lente hello per MySQL.</span><span class="sxs-lookup"><span data-stu-id="43c37-245">hello MySQL slow query log can help you identify hello slow queries for MySQL.</span></span> <span data-ttu-id="43c37-246">Dopo aver abilitato i log di query lente hello MySQL, è possibile usare strumenti di MySQL come **mysqldumpslow** tooidentify hello collo di bottiglia.</span><span class="sxs-lookup"><span data-stu-id="43c37-246">After enabling hello MySQL slow query log, you can use MySQL tools like **mysqldumpslow** tooidentify hello performance bottleneck.</span></span>  

<span data-ttu-id="43c37-247">Per impostazione log non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="43c37-247">By default, this is not enabled.</span></span> <span data-ttu-id="43c37-248">Accensione di log query lente hello può comportare l'utilizzo di alcune risorse di CPU.</span><span class="sxs-lookup"><span data-stu-id="43c37-248">Turning on hello slow query log might consume some CPU resources.</span></span> <span data-ttu-id="43c37-249">È consigliabile abilitarlo temporaneamente per la risoluzione dei colli di bottiglia delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="43c37-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="43c37-250">tooturn nel log query lente hello:</span><span class="sxs-lookup"><span data-stu-id="43c37-250">tooturn on hello slow query log:</span></span>

1. <span data-ttu-id="43c37-251">Modificare file my.cnf hello aggiungendo hello fine toohello le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="43c37-251">Modify hello my.cnf file by adding hello following lines toohello end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="43c37-252">Riavviare il server di MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="43c37-252">Restart hello MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="43c37-253">Controllare se l'impostazione hello è diventino effettive tramite hello **Mostra** comando.</span><span class="sxs-lookup"><span data-stu-id="43c37-253">Check whether hello setting is taking effect by using hello **show** command.</span></span>

![Slow-query-log ON][7]   

![Slow-query-log results][8]

<span data-ttu-id="43c37-256">In questo esempio, è possibile visualizzare che tale funzionalità di query lente hello è stata attivata.</span><span class="sxs-lookup"><span data-stu-id="43c37-256">In this example, you can see that hello slow query feature has been turned on.</span></span> <span data-ttu-id="43c37-257">È quindi possibile utilizzare hello **mysqldumpslow** strumento toodetermine i colli di bottiglia delle prestazioni e ottimizzare le prestazioni, ad esempio l'aggiunta di indici.</span><span class="sxs-lookup"><span data-stu-id="43c37-257">You can then use hello **mysqldumpslow** tool toodetermine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="43c37-258">Appendici</span><span class="sxs-lookup"><span data-stu-id="43c37-258">Appendices</span></span>
<span data-ttu-id="43c37-259">di seguito Hello sono dati di test delle prestazioni di esempio prodotti in un ambiente di laboratorio di destinazione.</span><span class="sxs-lookup"><span data-stu-id="43c37-259">hello following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="43c37-260">Forniscono informazioni generali sulla tendenza dei dati delle prestazioni di hello con approcci di ottimizzazione delle prestazioni diversi.</span><span class="sxs-lookup"><span data-stu-id="43c37-260">They provide general background on hello performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="43c37-261">Hello risultati potrebbero variare in versioni diverse di ambiente o il prodotto.</span><span class="sxs-lookup"><span data-stu-id="43c37-261">hello results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="43c37-262"><a name="AppendixA"></a>Appendice A</span><span class="sxs-lookup"><span data-stu-id="43c37-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="43c37-263">**Prestazioni del disco (IOPS) con livelli RAID diversi**</span><span class="sxs-lookup"><span data-stu-id="43c37-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![Prestazioni del disco (IOPS) con livelli RAID diversi][9]

<span data-ttu-id="43c37-265">**Comandi di test**</span><span class="sxs-lookup"><span data-stu-id="43c37-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="43c37-266">carico di lavoro Hello di questo test Usa 64 thread, durante il tentativo limite hello tooreach di RAID.</span><span class="sxs-lookup"><span data-stu-id="43c37-266">hello workload of this test uses 64 threads, trying tooreach hello upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="43c37-267"><a name="AppendixB"></a>Appendice B</span><span class="sxs-lookup"><span data-stu-id="43c37-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="43c37-268">**Confronto delle prestazioni (velocità effettiva) di MySQL con livelli RAID diversi** </span><span class="sxs-lookup"><span data-stu-id="43c37-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="43c37-269">(XFS file system)</span><span class="sxs-lookup"><span data-stu-id="43c37-269">(XFS file system)</span></span>

![Confronto delle prestazioni (OLTP) di MySQL con livelli RAID diversi][10]  
![Confronto delle prestazioni (OLTP) di MySQL con livelli RAID diversi][11]

<span data-ttu-id="43c37-272">**Comandi di test**</span><span class="sxs-lookup"><span data-stu-id="43c37-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="43c37-273">**Confronto delle prestazioni (OLTP) di MySQL con livelli RAID diversi**</span><span class="sxs-lookup"><span data-stu-id="43c37-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="43c37-274">![Confronto delle prestazioni (OLTP) di MySQL con livelli RAID diversi][12]</span><span class="sxs-lookup"><span data-stu-id="43c37-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="43c37-275">**Comandi di test**</span><span class="sxs-lookup"><span data-stu-id="43c37-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="43c37-276"><a name="AppendixC"></a>Appendice C</span><span class="sxs-lookup"><span data-stu-id="43c37-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="43c37-277">**Confronto delle prestazioni (IOPS) del disco per dimensioni del blocco diverse**</span><span class="sxs-lookup"><span data-stu-id="43c37-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="43c37-278">(XFS file system)</span><span class="sxs-lookup"><span data-stu-id="43c37-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="43c37-279">**Comandi di test**</span><span class="sxs-lookup"><span data-stu-id="43c37-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="43c37-280">utilizzato per la verifica delle dimensioni del file Hello 30 GB e 1 GB, rispettivamente, con RAID 0 (4 dischi) XFS file system.</span><span class="sxs-lookup"><span data-stu-id="43c37-280">hello file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="43c37-281"><a name="AppendixD"></a>Appendice D</span><span class="sxs-lookup"><span data-stu-id="43c37-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="43c37-282">**Confronto delle prestazioni (velocità effettiva) di MySQL prima e dopo l'ottimizzazione**</span><span class="sxs-lookup"><span data-stu-id="43c37-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="43c37-283">(XFS file system)</span><span class="sxs-lookup"><span data-stu-id="43c37-283">(XFS File System)</span></span>

![Confronto delle prestazioni (velocità effettiva) di MySQL prima e dopo l'ottimizzazione][14]

<span data-ttu-id="43c37-285">**Comandi di test**</span><span class="sxs-lookup"><span data-stu-id="43c37-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="43c37-286">**impostazione di configurazione Hello per impostazione predefinita e l'ottimizzazione è il seguente:**</span><span class="sxs-lookup"><span data-stu-id="43c37-286">**hello configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="43c37-287">parameters</span><span class="sxs-lookup"><span data-stu-id="43c37-287">Parameters</span></span> | <span data-ttu-id="43c37-288">Default</span><span class="sxs-lookup"><span data-stu-id="43c37-288">Default</span></span> | <span data-ttu-id="43c37-289">Ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="43c37-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="43c37-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="43c37-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="43c37-291">Nessuna</span><span class="sxs-lookup"><span data-stu-id="43c37-291">None</span></span> |<span data-ttu-id="43c37-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="43c37-292">7 GB</span></span> |
| <span data-ttu-id="43c37-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="43c37-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="43c37-294">5 MB</span><span class="sxs-lookup"><span data-stu-id="43c37-294">5 MB</span></span> |<span data-ttu-id="43c37-295">512 MB</span><span class="sxs-lookup"><span data-stu-id="43c37-295">512 MB</span></span> |
| <span data-ttu-id="43c37-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="43c37-296">**max_connections**</span></span> |<span data-ttu-id="43c37-297">100</span><span class="sxs-lookup"><span data-stu-id="43c37-297">100</span></span> |<span data-ttu-id="43c37-298">5000</span><span class="sxs-lookup"><span data-stu-id="43c37-298">5000</span></span> |
| <span data-ttu-id="43c37-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="43c37-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="43c37-300">0</span><span class="sxs-lookup"><span data-stu-id="43c37-300">0</span></span> |<span data-ttu-id="43c37-301">1</span><span class="sxs-lookup"><span data-stu-id="43c37-301">1</span></span> |
| <span data-ttu-id="43c37-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="43c37-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="43c37-303">1</span><span class="sxs-lookup"><span data-stu-id="43c37-303">1</span></span> |<span data-ttu-id="43c37-304">2</span><span class="sxs-lookup"><span data-stu-id="43c37-304">2</span></span> |
| <span data-ttu-id="43c37-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="43c37-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="43c37-306">8 MB</span><span class="sxs-lookup"><span data-stu-id="43c37-306">8 MB</span></span> |<span data-ttu-id="43c37-307">128 MB</span><span class="sxs-lookup"><span data-stu-id="43c37-307">128 MB</span></span> |
| <span data-ttu-id="43c37-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="43c37-308">**query_cache_size**</span></span> |<span data-ttu-id="43c37-309">16 MB</span><span class="sxs-lookup"><span data-stu-id="43c37-309">16 MB</span></span> |<span data-ttu-id="43c37-310">0</span><span class="sxs-lookup"><span data-stu-id="43c37-310">0</span></span> |

<span data-ttu-id="43c37-311">Per più dettagliate [i parametri di configurazione di ottimizzazione](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), fare riferimento toohello [istruzioni ufficiale MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="43c37-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer toohello [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="43c37-312">**Ambiente di test**</span><span class="sxs-lookup"><span data-stu-id="43c37-312">**Test environment**</span></span>  

| <span data-ttu-id="43c37-313">Hardware</span><span class="sxs-lookup"><span data-stu-id="43c37-313">Hardware</span></span> | <span data-ttu-id="43c37-314">Dettagli</span><span class="sxs-lookup"><span data-stu-id="43c37-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="43c37-315">CPU</span><span class="sxs-lookup"><span data-stu-id="43c37-315">CPU</span></span> |<span data-ttu-id="43c37-316">AMD Opteron(tm) Processore 4171 HE/4 core</span><span class="sxs-lookup"><span data-stu-id="43c37-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="43c37-317">Memoria</span><span class="sxs-lookup"><span data-stu-id="43c37-317">Memory</span></span> |<span data-ttu-id="43c37-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="43c37-318">14 GB</span></span> |
| <span data-ttu-id="43c37-319">Disco</span><span class="sxs-lookup"><span data-stu-id="43c37-319">Disk</span></span> |<span data-ttu-id="43c37-320">10 GB/disco</span><span class="sxs-lookup"><span data-stu-id="43c37-320">10 GB/disk</span></span> |
| <span data-ttu-id="43c37-321">OS</span><span class="sxs-lookup"><span data-stu-id="43c37-321">OS</span></span> |<span data-ttu-id="43c37-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="43c37-322">Ubuntu 14.04.1 LTS</span></span> |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

