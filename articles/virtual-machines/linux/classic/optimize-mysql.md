---
title: Ottimizzare le prestazioni di MySQL su Linux | Microsoft Docs
description: Informazioni su come ottimizzare MySQL in esecuzione su una macchina virtuale di Azure che esegue Linux.
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
ms.openlocfilehash: 8f2ec884fa98e989448ac11675e71f39aa21fa7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="3feff-103">Ottimizzare le prestazioni di MySQL in macchine virtuali Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="3feff-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="3feff-104">Esistono molti fattori che influiscono sulle prestazioni di MySQL in Azure, sia nella selezione dell'hardware virtuale sia nella configurazione software.</span><span class="sxs-lookup"><span data-stu-id="3feff-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="3feff-105">Questo articolo è incentrato sull'ottimizzazione delle prestazioni tramite la configurazione dell'archiviazione, del sistema e del database.</span><span class="sxs-lookup"><span data-stu-id="3feff-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3feff-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="3feff-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="3feff-107">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="3feff-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="3feff-108">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="3feff-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="3feff-109">Per informazioni sulle ottimizzazioni delle macchine virtuali Linux usando il modello di Resource Manager, vedere [Ottimizzare la VM Linux su Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3feff-109">For information about Linux VM optimizations with the Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="3feff-110">Usare RAID in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="3feff-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="3feff-111">L'archiviazione è il fattore che influisce maggiormente sulle prestazioni del database negli ambienti cloud.</span><span class="sxs-lookup"><span data-stu-id="3feff-111">Storage is the key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="3feff-112">Rispetto a un singolo disco, RAID può fornire un accesso più rapido tramite la concorrenza.</span><span class="sxs-lookup"><span data-stu-id="3feff-112">Compared to a single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="3feff-113">Per altre informazioni, vedere la pagina [Livelli RAID standard](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="3feff-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="3feff-114">Tramite RAID è possibile migliorare la velocità effettiva di I/O del disco e il tempo di risposta di I/O in Azure.</span><span class="sxs-lookup"><span data-stu-id="3feff-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="3feff-115">I test di laboratorio indicano che in media la velocità effettiva di I/O del disco può essere raddoppiata e il tempo di risposta di I/O può essere dimezzato raddoppiando il numero di dischi RAID (da due a quattro, da quattro a otto e così via).</span><span class="sxs-lookup"><span data-stu-id="3feff-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when the number of RAID disks is doubled (from two to four, four to eight, etc.).</span></span> <span data-ttu-id="3feff-116">Per informazioni dettagliate, vedere [Appendice A](#AppendixA) .</span><span class="sxs-lookup"><span data-stu-id="3feff-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="3feff-117">Oltre all'I/O del disco, aumentando il livello RAID migliorano anche le prestazioni di MySQL.</span><span class="sxs-lookup"><span data-stu-id="3feff-117">In addition to disk I/O, MySQL performance improves when you increase the RAID level.</span></span>  <span data-ttu-id="3feff-118">Per informazioni dettagliate, vedere [Appendice B](#AppendixB) .</span><span class="sxs-lookup"><span data-stu-id="3feff-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="3feff-119">Può inoltre essere utile prendere in considerazione le dimensioni del blocco.</span><span class="sxs-lookup"><span data-stu-id="3feff-119">You might also want to consider the chunk size.</span></span> <span data-ttu-id="3feff-120">In generale, con blocchi di dimensioni maggiori si ha un sovraccarico ridotto, soprattutto per le scritture di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="3feff-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="3feff-121">Tuttavia, blocchi di dimensioni troppo grandi potrebbero far aumentare il sovraccarico, rendendo impossibile l'uso del RAID.</span><span class="sxs-lookup"><span data-stu-id="3feff-121">However, when the chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="3feff-122">La dimensione predefinita corrente, dimostratasi ottimale per la maggior parte degli ambienti di produzione, è pari a 512 KB.</span><span class="sxs-lookup"><span data-stu-id="3feff-122">The current default size is 512 KB, which is proven to be optimal for most general production environments.</span></span> <span data-ttu-id="3feff-123">Per informazioni dettagliate, vedere [Appendice C](#AppendixC) .</span><span class="sxs-lookup"><span data-stu-id="3feff-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="3feff-124">Esistono limiti al numero di dischi che è possibile aggiungere per i diversi tipi di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3feff-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="3feff-125">Questi limiti sono descritti in dettaglio in [Dimensioni delle macchine virtuali e dei servizi cloud per Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="3feff-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="3feff-126">Per l'esempio RAID proposto in questo articolo si dovrà disporre di quattro dischi dati collegati, anche se è possibile scegliere di configurare RAID con un numero di dischi inferiore.</span><span class="sxs-lookup"><span data-stu-id="3feff-126">You will need four attached data disks to follow the RAID example in this article, although you can choose to set up RAID with fewer disks.</span></span>  

<span data-ttu-id="3feff-127">In questo articolo si presuppone che l'utente abbia già creato una macchina virtuale Linux e che MYSQL sia già stato installato e configurato.</span><span class="sxs-lookup"><span data-stu-id="3feff-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="3feff-128">Per altre informazioni, vedere la documentazione sulle modalità di installazione di MySQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="3feff-128">For more information on getting started, see How to install MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="3feff-129">Configurare RAID in Azure</span><span class="sxs-lookup"><span data-stu-id="3feff-129">Set up RAID on Azure</span></span>
<span data-ttu-id="3feff-130">La procedura seguente illustra la creazione di RAID in Azure tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3feff-130">The following steps show how to create RAID on Azure by using the Azure portal.</span></span> <span data-ttu-id="3feff-131">È inoltre possibile configurare RAID usando gli script di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3feff-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="3feff-132">In questo esempio verrà configurato RAID 0 con quattro dischi.</span><span class="sxs-lookup"><span data-stu-id="3feff-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-to-your-virtual-machine"></a><span data-ttu-id="3feff-133">Aggiungere un disco dati alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3feff-133">Add a data disk to your virtual machine</span></span>
<span data-ttu-id="3feff-134">Nel portale di Azure accedere al dashboard e selezionare la macchina virtuale a cui si vuole aggiungere un disco dati.</span><span class="sxs-lookup"><span data-stu-id="3feff-134">In the Azure portal, go to the dashboard and select the virtual machine to which you want to add a data disk.</span></span> <span data-ttu-id="3feff-135">In questo esempio la macchina virtuale è mysqlnode1.</span><span class="sxs-lookup"><span data-stu-id="3feff-135">In this example, the virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="3feff-136">Fare clic su **Dischi** e quindi su **Collega nuovo**.</span><span class="sxs-lookup"><span data-stu-id="3feff-136">Click **Disks** and then click **Attach New**.</span></span>

![Aggiunta di dischi nelle macchine virtuali](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="3feff-138">Creare un nuovo disco da 500 GB.</span><span class="sxs-lookup"><span data-stu-id="3feff-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="3feff-139">Assicurarsi che **Preferenze cache dell'host** sia impostato su **Nessuna**.</span><span class="sxs-lookup"><span data-stu-id="3feff-139">Make sure that **Host Cache Preference** is set to **None**.</span></span>  <span data-ttu-id="3feff-140">Al termine, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3feff-140">When you're finished, click **OK**.</span></span>

![Attach Empty Disk](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="3feff-142">Verrà aggiunto un disco vuoto nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3feff-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="3feff-143">Ripetere questo passaggio tre volte in modo da disporre di quattro dischi dati per RAID.</span><span class="sxs-lookup"><span data-stu-id="3feff-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="3feff-144">È possibile visualizzare le unità aggiunte nella macchina virtuale esaminando il log dei messaggi del kernel.</span><span class="sxs-lookup"><span data-stu-id="3feff-144">You can see the added drives in the virtual machine by looking at the kernel message log.</span></span> <span data-ttu-id="3feff-145">Ad esempio, per visualizzarlo in Ubuntu, usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="3feff-145">For example, to see this on Ubuntu, use the following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-the-additional-disks"></a><span data-ttu-id="3feff-146">Creare RAID con i dischi aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="3feff-146">Create RAID with the additional disks</span></span>
<span data-ttu-id="3feff-147">I seguenti passaggi illustrano come [configurare RAID software in Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3feff-147">The following steps describe how to [configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="3feff-148">Se si usa il file system XFS, eseguire la seguente procedura dopo aver creato RAID.</span><span class="sxs-lookup"><span data-stu-id="3feff-148">If you are using the XFS file system, execute the following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="3feff-149">Per installare XFS su Debian, Ubuntu o Linux Mint, usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="3feff-149">To install XFS on Debian, Ubuntu, or Linux Mint, use the following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="3feff-150">Per installare XFS su Fedora, CentOS o RHEL, usare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="3feff-150">To install XFS on Fedora, CentOS, or RHEL, use the following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="3feff-151">Impostare un nuovo percorso di archiviazione</span><span class="sxs-lookup"><span data-stu-id="3feff-151">Set up a new storage path</span></span>
<span data-ttu-id="3feff-152">Usare il comando seguente per impostare un nuovo percorso di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="3feff-152">Use the following command to set up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-the-original-data-to-the-new-storage-path"></a><span data-ttu-id="3feff-153">Copiare i dati originali nel nuovo percorso di archiviazione</span><span class="sxs-lookup"><span data-stu-id="3feff-153">Copy the original data to the new storage path</span></span>
<span data-ttu-id="3feff-154">Usare il comando seguente per copiare dati nel nuovo percorso di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="3feff-154">Use the following command to copy data to the new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-the-data-disk"></a><span data-ttu-id="3feff-155">Modificare le autorizzazioni in modo che MySQL possa avere accesso in lettura e in scrittura al disco dati</span><span class="sxs-lookup"><span data-stu-id="3feff-155">Modify permissions so MySQL can access (read and write) the data disk</span></span>
<span data-ttu-id="3feff-156">Usare il comando seguente per modificare le autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="3feff-156">Use the following command to modify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-the-disk-io-scheduling-algorithm"></a><span data-ttu-id="3feff-157">Modificare l'algoritmo di pianificazione di I/O del disco</span><span class="sxs-lookup"><span data-stu-id="3feff-157">Adjust the disk I/O scheduling algorithm</span></span>
<span data-ttu-id="3feff-158">Linux implementa quattro tipi di algoritmi di pianificazione di I/O:</span><span class="sxs-lookup"><span data-stu-id="3feff-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="3feff-159">Algoritmo NOOP (Nessuna operazione)</span><span class="sxs-lookup"><span data-stu-id="3feff-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="3feff-160">Algoritmo di scadenza (Scadenza)</span><span class="sxs-lookup"><span data-stu-id="3feff-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="3feff-161">Algoritmo di accodamento pienamente equo (CFQ, Completely fair queuing)</span><span class="sxs-lookup"><span data-stu-id="3feff-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="3feff-162">Algoritmo del periodo di budget (Anticipatorio)</span><span class="sxs-lookup"><span data-stu-id="3feff-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="3feff-163">Per ottimizzare le prestazioni è possibile selezionare diverse utilità di pianificazione di I/O in scenari diversi.</span><span class="sxs-lookup"><span data-stu-id="3feff-163">You can select different I/O schedulers under different scenarios to optimize performance.</span></span> <span data-ttu-id="3feff-164">In un ambiente ad accesso completamente casuale non esiste una differenza significativa tra gli algoritmi CFQ e di scadenza a livello di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="3feff-164">In a completely random access environment, there is not a significant difference between the CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="3feff-165">È consigliabile impostare l'ambiente del database MySQL sull'algoritmo di scadenza per maggiore stabilità.</span><span class="sxs-lookup"><span data-stu-id="3feff-165">We recommend that you set the MySQL database environment to Deadline for stability.</span></span> <span data-ttu-id="3feff-166">Se è presente un I/O sequenziale considerevole, l'algoritmo CFQ potrebbe ridurre le prestazioni di I/O del disco.</span><span class="sxs-lookup"><span data-stu-id="3feff-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="3feff-167">Per le unità SSD e altri dispositivi, con gli algoritmi NOOP o di scadenza è possibile ottenere prestazioni migliori rispetto all'utilità di pianificazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="3feff-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than the default scheduler.</span></span>   

<span data-ttu-id="3feff-168">Prima del kernel 2.5, l'algoritmo di pianificazione di I/O predefinito è quello di scadenza.</span><span class="sxs-lookup"><span data-stu-id="3feff-168">Prior to the kernel 2.5, the default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="3feff-169">A partire dal kernel 2.6.18, l'algoritmo CFQ è diventato l'algoritmo di pianificazione di I/O predefinito.</span><span class="sxs-lookup"><span data-stu-id="3feff-169">Starting with the kernel 2.6.18, CFQ became the default I/O scheduling algorithm.</span></span>  <span data-ttu-id="3feff-170">È possibile specificare questa impostazione in fase di avvio del kernel oppure modificarla in maniera dinamica mentre il sistema è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3feff-170">You can specify this setting at kernel boot time or dynamically modify this setting when the system is running.</span></span>  

<span data-ttu-id="3feff-171">Il seguente esempio mostra come controllare e impostare l'utilità di pianificazione predefinita per l'algoritmo NOOP nel gruppo di distribuzione Debian.</span><span class="sxs-lookup"><span data-stu-id="3feff-171">The following example demonstrates how to check and set the default scheduler to the NOOP algorithm in the Debian distribution family.</span></span>  

### <a name="view-the-current-io-scheduler"></a><span data-ttu-id="3feff-172">Visualizzare l'utilità di pianificazione di I/O corrente</span><span class="sxs-lookup"><span data-stu-id="3feff-172">View the current I/O scheduler</span></span>
<span data-ttu-id="3feff-173">Per visualizzare l'utilità di pianificazione, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3feff-173">To view the scheduler run the following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="3feff-174">Si visualizzerà il seguente output, che indica l'utilità di pianificazione corrente:</span><span class="sxs-lookup"><span data-stu-id="3feff-174">You will see following output, which indicates the current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-the-current-device-devsda-of-the-io-scheduling-algorithm"></a><span data-ttu-id="3feff-175">Modificare il dispositivo corrente (/dev/sda) dell'algoritmo di pianificazione di I/O</span><span class="sxs-lookup"><span data-stu-id="3feff-175">Change the current device (/dev/sda) of the I/O scheduling algorithm</span></span>
<span data-ttu-id="3feff-176">Eseguire i comandi seguenti per cambiare il dispositivo corrente:</span><span class="sxs-lookup"><span data-stu-id="3feff-176">Run the following commands to change the current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="3feff-177">Impostare questa opzione solo per /dev/sda è inutile.</span><span class="sxs-lookup"><span data-stu-id="3feff-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="3feff-178">L'opzione deve essere impostata su tutti i dischi dati in cui si trova il database.</span><span class="sxs-lookup"><span data-stu-id="3feff-178">It must be set on all data disks where the database resides.</span></span>  
>
>

<span data-ttu-id="3feff-179">Si dovrebbe visualizzare il seguente output, che indica che grub.cfg è stato ricreato correttamente e che l'utilità di pianificazione predefinita è stata impostata su NOOP:</span><span class="sxs-lookup"><span data-stu-id="3feff-179">You should see the following output, indicating that grub.cfg has been rebuilt successfully and that the default scheduler has been updated to NOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="3feff-180">Per il gruppo di distribuzione Redhat è necessario solo il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="3feff-180">For the Red Hat distribution family, you need only the following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="3feff-181">Configurare le impostazioni per le operazioni del file system</span><span class="sxs-lookup"><span data-stu-id="3feff-181">Configure system file operations settings</span></span>
<span data-ttu-id="3feff-182">Una delle procedure consigliate consiste nel disabilitare la funzionalità di registrazione dell'*atime* nel file system.</span><span class="sxs-lookup"><span data-stu-id="3feff-182">One best practice is to disable the *atime* logging feature on the file system.</span></span> <span data-ttu-id="3feff-183">L'atime è l'ora dell'ultimo accesso al file.</span><span class="sxs-lookup"><span data-stu-id="3feff-183">Atime is the last file access time.</span></span> <span data-ttu-id="3feff-184">Ogni volta che si accede a un file, il file system registra il timestamp nel log.</span><span class="sxs-lookup"><span data-stu-id="3feff-184">Whenever a file is accessed, the file system records the timestamp in the log.</span></span> <span data-ttu-id="3feff-185">Tuttavia, queste informazioni vengono usate raramente.</span><span class="sxs-lookup"><span data-stu-id="3feff-185">However, this information is rarely used.</span></span> <span data-ttu-id="3feff-186">Se non è necessaria, è possibile disabilitare questa opzione, riducendo così il tempo complessivo di accesso al disco.</span><span class="sxs-lookup"><span data-stu-id="3feff-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="3feff-187">Per disattivare la registrazione dell'atime, è necessario modificare il file di configurazione del file system /etc/. fstab e aggiungere l'opzione **noatime**.</span><span class="sxs-lookup"><span data-stu-id="3feff-187">To disable atime logging, you need to modify the file system configuration file /etc/ fstab and add the **noatime** option.</span></span>  

<span data-ttu-id="3feff-188">Modificare ad esempio il file vim /etc/fstab aggiungendo l'opzione noatime come illustrato nell'esempio di seguito:</span><span class="sxs-lookup"><span data-stu-id="3feff-188">For example, edit the vim /etc/fstab file, adding the noatime as shown in the following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by the Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add the “noatime” option below to disable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="3feff-189">Rimontare il file system con il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="3feff-189">Then, remount the file system with the following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="3feff-190">Verificare il risultato modificato.</span><span class="sxs-lookup"><span data-stu-id="3feff-190">Test the modified result.</span></span> <span data-ttu-id="3feff-191">Quando si modifica il file di test, il tempo di accesso non viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="3feff-191">When you modify the test file, the access time is not updated.</span></span> <span data-ttu-id="3feff-192">Negli esempi seguenti viene illustrano l'aspetto del codice prima e dopo la modifica.</span><span class="sxs-lookup"><span data-stu-id="3feff-192">The following examples show what the code looks like before and after modification.</span></span>

<span data-ttu-id="3feff-193">Prima:</span><span class="sxs-lookup"><span data-stu-id="3feff-193">Before:</span></span>        

![Codice prima delle modifiche di accesso][5]

<span data-ttu-id="3feff-195">Dopo:</span><span class="sxs-lookup"><span data-stu-id="3feff-195">After:</span></span>

![Codice dopo le modifiche di accesso][6]

## <a name="increase-the-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="3feff-197">Aumentare il numero massimo di handle di sistema per la concorrenza elevata</span><span class="sxs-lookup"><span data-stu-id="3feff-197">Increase the maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="3feff-198">MySQL è un database a concorrenza elevata.</span><span class="sxs-lookup"><span data-stu-id="3feff-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="3feff-199">Il numero predefinito di handle simultanei per Linux è pari a 1024, ma non sempre è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="3feff-199">The default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="3feff-200">Eseguire la seguente procedura per aumentare il numero massimo di handle simultanei del sistema, in modo da supportare la concorrenza elevata di MySQL.</span><span class="sxs-lookup"><span data-stu-id="3feff-200">Use the following steps to increase the maximum concurrent handles of the system to support high concurrency of MySQL.</span></span>

### <a name="modify-the-limitsconf-file"></a><span data-ttu-id="3feff-201">Modificare il file limits.conf</span><span class="sxs-lookup"><span data-stu-id="3feff-201">Modify the limits.conf file</span></span>
<span data-ttu-id="3feff-202">Aggiungere le seguenti quattro righe nel file /etc/security/limits.conf per aumentare il numero massimo di handle simultanei consentiti.</span><span class="sxs-lookup"><span data-stu-id="3feff-202">To increase the maximum allowed concurrent handles, add the following four lines in the /etc/security/limits.conf file.</span></span> <span data-ttu-id="3feff-203">Si noti che 65536 è il numero massimo di handle che il sistema è in grado di supportare.</span><span class="sxs-lookup"><span data-stu-id="3feff-203">Note that 65536 is the maximum number that the system can support.</span></span>   

    * <span data-ttu-id="3feff-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="3feff-204">soft nofile 65536</span></span>
    * <span data-ttu-id="3feff-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="3feff-205">hard nofile 65536</span></span>
    * <span data-ttu-id="3feff-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="3feff-206">soft nproc 65536</span></span>
    * <span data-ttu-id="3feff-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="3feff-207">hard nproc 65536</span></span>

### <a name="update-the-system-for-the-new-limits"></a><span data-ttu-id="3feff-208">Aggiornare il sistema con i nuovi limiti</span><span class="sxs-lookup"><span data-stu-id="3feff-208">Update the system for the new limits</span></span>
<span data-ttu-id="3feff-209">Per aggiornare il sistema, eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3feff-209">To update the system, run the following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-the-limits-are-updated-at-boot-time"></a><span data-ttu-id="3feff-210">Assicurarsi che i limiti vengano aggiornati in fase di avvio</span><span class="sxs-lookup"><span data-stu-id="3feff-210">Ensure that the limits are updated at boot time</span></span>
<span data-ttu-id="3feff-211">Immettere i seguenti comandi di avvio nel file /etc/rc.local in modo che la modifica sia applicata all'avvio.</span><span class="sxs-lookup"><span data-stu-id="3feff-211">Put the following startup commands in the /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="3feff-212">Ottimizzare il database MySQL</span><span class="sxs-lookup"><span data-stu-id="3feff-212">MySQL database optimization</span></span>
<span data-ttu-id="3feff-213">Per configurare MySQL in Azure è possibile usare la stessa strategia di ottimizzazione delle prestazioni di un computer locale.</span><span class="sxs-lookup"><span data-stu-id="3feff-213">To configure MySQL on Azure, you can use the same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="3feff-214">Le principali regole di ottimizzazione di I/O sono:</span><span class="sxs-lookup"><span data-stu-id="3feff-214">The main I/O optimization rules are:</span></span>   

* <span data-ttu-id="3feff-215">Aumentare la dimensione della cache.</span><span class="sxs-lookup"><span data-stu-id="3feff-215">Increase the cache size.</span></span>
* <span data-ttu-id="3feff-216">Ridurre il tempo di risposta di I/O.</span><span class="sxs-lookup"><span data-stu-id="3feff-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="3feff-217">Per ottimizzare le impostazioni del server MySQL, è possibile aggiornare il file my.cnf, ovvero il file di configurazione predefinito per i computer server e client.</span><span class="sxs-lookup"><span data-stu-id="3feff-217">To optimize MySQL server settings, you can update the my.cnf file, which is the default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="3feff-218">I seguenti elementi di configurazione sono i principali fattori che influiscono sulle prestazioni di MySQL:</span><span class="sxs-lookup"><span data-stu-id="3feff-218">The following configuration items are the main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="3feff-219">**innodb_buffer_pool_size**: il pool di buffer contiene i dati memorizzati nel buffer e l'indice.</span><span class="sxs-lookup"><span data-stu-id="3feff-219">**innodb_buffer_pool_size**: The buffer pool contains buffered data and the index.</span></span> <span data-ttu-id="3feff-220">In genere è impostato al 70% della memoria fisica.</span><span class="sxs-lookup"><span data-stu-id="3feff-220">This is usually set to 70 percent of physical memory.</span></span>
* <span data-ttu-id="3feff-221">**innodb_log_file_size**: la dimensione del log di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3feff-221">**innodb_log_file_size**: This is the redo log size.</span></span> <span data-ttu-id="3feff-222">È possibile usare i log di ripristino per assicurare che le operazioni di scrittura siano veloci, affidabili e recuperabili dopo un arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="3feff-222">You use redo logs to ensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="3feff-223">È impostato su 512 MB, pertanto sarà disponibile una notevole quantità di spazio per la registrazione delle operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="3feff-223">This is set to 512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="3feff-224">**max_connections**: in alcuni casi le applicazioni non chiudono correttamente le connessioni.</span><span class="sxs-lookup"><span data-stu-id="3feff-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="3feff-225">Un valore più elevato garantirà al server più tempo per riciclare le connessioni inattive.</span><span class="sxs-lookup"><span data-stu-id="3feff-225">A larger value will give the server more time to recycle idled connections.</span></span> <span data-ttu-id="3feff-226">Il numero massimo di connessioni è 10.000, ma quello consigliato è 5.000.</span><span class="sxs-lookup"><span data-stu-id="3feff-226">The maximum number of connections is 10,000, but the recommended maximum is 5,000.</span></span>
* <span data-ttu-id="3feff-227">**Innodb_file_per_table**: questa impostazione consente di abilitare o disabilitare la capacità di InnoDB di archiviare le tabelle in file separati.</span><span class="sxs-lookup"><span data-stu-id="3feff-227">**Innodb_file_per_table**: This setting enables or disables the ability of InnoDB to store tables in separate files.</span></span> <span data-ttu-id="3feff-228">Una volta attiva, l'opzione assicura che le diverse operazioni avanzate di amministrazione vengano eseguite in modo efficiente.</span><span class="sxs-lookup"><span data-stu-id="3feff-228">Turn on the option to ensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="3feff-229">Dal punto di vista delle prestazioni, può velocizzare la trasmissione degli spazi di tabella e ottimizzare le prestazioni della gestione dei detriti.</span><span class="sxs-lookup"><span data-stu-id="3feff-229">From a performance point of view, it can speed up the table space transmission and optimize the debris management performance.</span></span> <span data-ttu-id="3feff-230">L'impostazione consigliata è ON.</span><span class="sxs-lookup"><span data-stu-id="3feff-230">The recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="3feff-231">Da MySQL 5.6, l'impostazione predefinita è ON, pertanto non è necessaria alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="3feff-231">From MySQL 5.6, the default setting is ON, so no action is required.</span></span> <span data-ttu-id="3feff-232">Per le versioni precedenti, l'impostazione predefinita è OFF.</span><span class="sxs-lookup"><span data-stu-id="3feff-232">For earlier versions, the default setting is OFF.</span></span> <span data-ttu-id="3feff-233">ed è necessario modificarla prima del caricamento dati, in quanto si applica solo alle tabelle appena create.</span><span class="sxs-lookup"><span data-stu-id="3feff-233">The setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="3feff-234">**innodb_flush_log_at_trx_commit**: il valore predefinito è 1, con l'ambito impostato su 0~2.</span><span class="sxs-lookup"><span data-stu-id="3feff-234">**innodb_flush_log_at_trx_commit**: The default value is 1, with the scope set to 0~2.</span></span> <span data-ttu-id="3feff-235">Il valore predefinito è l'opzione più adatta per il database MySQL come pacchetto autonomo.</span><span class="sxs-lookup"><span data-stu-id="3feff-235">The default value is the most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="3feff-236">Se impostato su 2, il valore assicura la massima integrità dei dati ed è appropriato per il server Master nel cluster MySQL.</span><span class="sxs-lookup"><span data-stu-id="3feff-236">The setting of 2 enables the most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="3feff-237">Se impostato su 0, il valore tollera la perdita di dati e questo può influire sulla affidabilità, garantendo in alcuni casi prestazioni migliori. Il valore 0 è appropriato per il server Slave nel cluster MySQL.</span><span class="sxs-lookup"><span data-stu-id="3feff-237">The setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="3feff-238">**Innodb_log_buffer_size**: il buffer del log consente l'esecuzione delle transazioni senza scaricare il log sul disco prima del commit delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="3feff-238">**Innodb_log_buffer_size**: The log buffer allows transactions to run without having to flush the log to disk before the transactions commit.</span></span> <span data-ttu-id="3feff-239">Tuttavia, se è presente un oggetto binario o un campo di testo di grandi dimensioni, la cache verrà usata rapidamente e verrà attivato un I/O frequente del disco.</span><span class="sxs-lookup"><span data-stu-id="3feff-239">However, if there is large binary object or text field, the cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="3feff-240">Se la variabile di stato Innodb_log_waits è diversa da 0, è consigliabile aumentare le dimensioni del buffer.</span><span class="sxs-lookup"><span data-stu-id="3feff-240">It is better increase the buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="3feff-241">**query_cache_size**: è consigliabile disabilitare questa opzione fin dall'inizio.</span><span class="sxs-lookup"><span data-stu-id="3feff-241">**query_cache_size**: The best option is to disable it from the outset.</span></span> <span data-ttu-id="3feff-242">Impostare query_cache_size su 0 (in MySQL 5.6 questa è l'impostazione predefinita) e usare altri metodi per velocizzare le query.</span><span class="sxs-lookup"><span data-stu-id="3feff-242">Set query_cache_size to 0 (this is the default setting in MySQL 5.6) and use other methods to speed up queries.</span></span>  

<span data-ttu-id="3feff-243">Vedere l'[Appendice D](#AppendixD) per un confronto delle prestazioni prima e dopo l'ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="3feff-243">See [Appendix D](#AppendixD) for a comparison of performance before and after the optimization.</span></span>

## <a name="turn-on-the-mysql-slow-query-log-for-analyzing-the-performance-bottleneck"></a><span data-ttu-id="3feff-244">Attivare il log di query lente di MySQL per l'analisi del collo di bottiglia delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="3feff-244">Turn on the MySQL slow query log for analyzing the performance bottleneck</span></span>
<span data-ttu-id="3feff-245">Il log di query lente di MySQL consente di identificare le query lente per MySQL.</span><span class="sxs-lookup"><span data-stu-id="3feff-245">The MySQL slow query log can help you identify the slow queries for MySQL.</span></span> <span data-ttu-id="3feff-246">Dopo l'abilitazione del log di query lente di MySQL, è possibile usare strumenti di MySQL come **mysqldumpslow** per identificare il collo di bottiglia delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="3feff-246">After enabling the MySQL slow query log, you can use MySQL tools like **mysqldumpslow** to identify the performance bottleneck.</span></span>  

<span data-ttu-id="3feff-247">Per impostazione log non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="3feff-247">By default, this is not enabled.</span></span> <span data-ttu-id="3feff-248">L'attivazione del log di query lente potrebbe usare alcune risorse della CPU.</span><span class="sxs-lookup"><span data-stu-id="3feff-248">Turning on the slow query log might consume some CPU resources.</span></span> <span data-ttu-id="3feff-249">È consigliabile abilitarlo temporaneamente per la risoluzione dei colli di bottiglia delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="3feff-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="3feff-250">Per attivare il log di query lente:</span><span class="sxs-lookup"><span data-stu-id="3feff-250">To turn on the slow query log:</span></span>

1. <span data-ttu-id="3feff-251">Modificare il file my.cnf aggiungendo alla fine del file le seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="3feff-251">Modify the my.cnf file by adding the following lines to the end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="3feff-252">Riavviare il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="3feff-252">Restart the MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="3feff-253">Verificare se l'impostazione è stata applicata tramite il comando **show**.</span><span class="sxs-lookup"><span data-stu-id="3feff-253">Check whether the setting is taking effect by using the **show** command.</span></span>

![Slow-query-log ON][7]   

![Slow-query-log results][8]

<span data-ttu-id="3feff-256">Come si può vedere, in questo esempio è stata attivata la funzionalità relativa alle query lente.</span><span class="sxs-lookup"><span data-stu-id="3feff-256">In this example, you can see that the slow query feature has been turned on.</span></span> <span data-ttu-id="3feff-257">È quindi possibile usare lo strumento **mysqldumpslow** per individuare i colli di bottiglia delle prestazioni e ottimizzare le prestazioni, ad esempio aggiungendo indici.</span><span class="sxs-lookup"><span data-stu-id="3feff-257">You can then use the **mysqldumpslow** tool to determine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="3feff-258">Appendici</span><span class="sxs-lookup"><span data-stu-id="3feff-258">Appendices</span></span>
<span data-ttu-id="3feff-259">Di seguito sono riportati i dati di esempio dei test sulle prestazioni prodotti nell'ambiente di destinazione,</span><span class="sxs-lookup"><span data-stu-id="3feff-259">The following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="3feff-260">che forniscono informazioni generali sulla tendenza dei dati delle prestazioni con i diversi approcci di ottimizzazione delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="3feff-260">They provide general background on the performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="3feff-261">I risultati possono tuttavia variare in ambienti o versioni di prodotto diverse.</span><span class="sxs-lookup"><span data-stu-id="3feff-261">The results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="3feff-262"><a name="AppendixA"></a>Appendice A</span><span class="sxs-lookup"><span data-stu-id="3feff-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="3feff-263">**Prestazioni del disco (IOPS) con livelli RAID diversi**</span><span class="sxs-lookup"><span data-stu-id="3feff-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![Prestazioni del disco (IOPS) con livelli RAID diversi][9]

<span data-ttu-id="3feff-265">**Comandi di test**</span><span class="sxs-lookup"><span data-stu-id="3feff-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="3feff-266">Il carico di lavoro di questo test usa 64 thread, al fine di raggiungere il limite massimo di RAID.</span><span class="sxs-lookup"><span data-stu-id="3feff-266">The workload of this test uses 64 threads, trying to reach the upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="3feff-267"><a name="AppendixB"></a>Appendice B</span><span class="sxs-lookup"><span data-stu-id="3feff-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="3feff-268">**Confronto delle prestazioni (velocità effettiva) di MySQL con livelli RAID diversi** </span><span class="sxs-lookup"><span data-stu-id="3feff-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="3feff-269">(XFS file system)</span><span class="sxs-lookup"><span data-stu-id="3feff-269">(XFS file system)</span></span>

![Confronto delle prestazioni (OLTP) di MySQL con livelli RAID diversi][10]  
![Confronto delle prestazioni (OLTP) di MySQL con livelli RAID diversi][11]

<span data-ttu-id="3feff-272">**Comandi di test**</span><span class="sxs-lookup"><span data-stu-id="3feff-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="3feff-273">**Confronto delle prestazioni (OLTP) di MySQL con livelli RAID diversi**</span><span class="sxs-lookup"><span data-stu-id="3feff-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="3feff-274">![Confronto delle prestazioni (OLTP) di MySQL con livelli RAID diversi][12]</span><span class="sxs-lookup"><span data-stu-id="3feff-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="3feff-275">**Comandi di test**</span><span class="sxs-lookup"><span data-stu-id="3feff-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="3feff-276"><a name="AppendixC"></a>Appendice C</span><span class="sxs-lookup"><span data-stu-id="3feff-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="3feff-277">**Confronto delle prestazioni (IOPS) del disco per dimensioni del blocco diverse**</span><span class="sxs-lookup"><span data-stu-id="3feff-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="3feff-278">(XFS file system)</span><span class="sxs-lookup"><span data-stu-id="3feff-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="3feff-279">**Comandi di test**</span><span class="sxs-lookup"><span data-stu-id="3feff-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="3feff-280">Le dimensioni del file usato per il test sono pari rispettivamente a 30 GB e 1 GB, con file system XFS RAID 0 (4 dischi).</span><span class="sxs-lookup"><span data-stu-id="3feff-280">The file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="3feff-281"><a name="AppendixD"></a>Appendice D</span><span class="sxs-lookup"><span data-stu-id="3feff-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="3feff-282">**Confronto delle prestazioni (velocità effettiva) di MySQL prima e dopo l'ottimizzazione**</span><span class="sxs-lookup"><span data-stu-id="3feff-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="3feff-283">(XFS file system)</span><span class="sxs-lookup"><span data-stu-id="3feff-283">(XFS File System)</span></span>

![Confronto delle prestazioni (velocità effettiva) di MySQL prima e dopo l'ottimizzazione][14]

<span data-ttu-id="3feff-285">**Comandi di test**</span><span class="sxs-lookup"><span data-stu-id="3feff-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="3feff-286">**L'impostazione di configurazione per impostazione predefinita e per l'ottimizzazione è la seguente:**</span><span class="sxs-lookup"><span data-stu-id="3feff-286">**The configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="3feff-287">Parametri</span><span class="sxs-lookup"><span data-stu-id="3feff-287">Parameters</span></span> | <span data-ttu-id="3feff-288">Default</span><span class="sxs-lookup"><span data-stu-id="3feff-288">Default</span></span> | <span data-ttu-id="3feff-289">Ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="3feff-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3feff-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="3feff-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="3feff-291">Nessuna</span><span class="sxs-lookup"><span data-stu-id="3feff-291">None</span></span> |<span data-ttu-id="3feff-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="3feff-292">7 GB</span></span> |
| <span data-ttu-id="3feff-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="3feff-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="3feff-294">5 MB</span><span class="sxs-lookup"><span data-stu-id="3feff-294">5 MB</span></span> |<span data-ttu-id="3feff-295">512 MB</span><span class="sxs-lookup"><span data-stu-id="3feff-295">512 MB</span></span> |
| <span data-ttu-id="3feff-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="3feff-296">**max_connections**</span></span> |<span data-ttu-id="3feff-297">100</span><span class="sxs-lookup"><span data-stu-id="3feff-297">100</span></span> |<span data-ttu-id="3feff-298">5000</span><span class="sxs-lookup"><span data-stu-id="3feff-298">5000</span></span> |
| <span data-ttu-id="3feff-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="3feff-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="3feff-300">0</span><span class="sxs-lookup"><span data-stu-id="3feff-300">0</span></span> |<span data-ttu-id="3feff-301">1</span><span class="sxs-lookup"><span data-stu-id="3feff-301">1</span></span> |
| <span data-ttu-id="3feff-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="3feff-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="3feff-303">1</span><span class="sxs-lookup"><span data-stu-id="3feff-303">1</span></span> |<span data-ttu-id="3feff-304">2</span><span class="sxs-lookup"><span data-stu-id="3feff-304">2</span></span> |
| <span data-ttu-id="3feff-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="3feff-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="3feff-306">8 MB</span><span class="sxs-lookup"><span data-stu-id="3feff-306">8 MB</span></span> |<span data-ttu-id="3feff-307">128 MB</span><span class="sxs-lookup"><span data-stu-id="3feff-307">128 MB</span></span> |
| <span data-ttu-id="3feff-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="3feff-308">**query_cache_size**</span></span> |<span data-ttu-id="3feff-309">16 MB</span><span class="sxs-lookup"><span data-stu-id="3feff-309">16 MB</span></span> |<span data-ttu-id="3feff-310">0</span><span class="sxs-lookup"><span data-stu-id="3feff-310">0</span></span> |

<span data-ttu-id="3feff-311">Per [parametri di configurazione dell'ottimizzazione](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html) più dettagliati, fare riferimento alle [istruzioni ufficiali di MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="3feff-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer to the [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="3feff-312">**Ambiente di test**</span><span class="sxs-lookup"><span data-stu-id="3feff-312">**Test environment**</span></span>  

| <span data-ttu-id="3feff-313">Hardware</span><span class="sxs-lookup"><span data-stu-id="3feff-313">Hardware</span></span> | <span data-ttu-id="3feff-314">Dettagli</span><span class="sxs-lookup"><span data-stu-id="3feff-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="3feff-315">CPU</span><span class="sxs-lookup"><span data-stu-id="3feff-315">CPU</span></span> |<span data-ttu-id="3feff-316">AMD Opteron(tm) Processore 4171 HE/4 core</span><span class="sxs-lookup"><span data-stu-id="3feff-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="3feff-317">Memoria</span><span class="sxs-lookup"><span data-stu-id="3feff-317">Memory</span></span> |<span data-ttu-id="3feff-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="3feff-318">14 GB</span></span> |
| <span data-ttu-id="3feff-319">Disco</span><span class="sxs-lookup"><span data-stu-id="3feff-319">Disk</span></span> |<span data-ttu-id="3feff-320">10 GB/disco</span><span class="sxs-lookup"><span data-stu-id="3feff-320">10 GB/disk</span></span> |
| <span data-ttu-id="3feff-321">OS</span><span class="sxs-lookup"><span data-stu-id="3feff-321">OS</span></span> |<span data-ttu-id="3feff-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="3feff-322">Ubuntu 14.04.1 LTS</span></span> |

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

