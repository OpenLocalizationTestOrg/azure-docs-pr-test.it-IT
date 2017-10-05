---
title: Nomi di dispositivo della macchina virtuale Linux modificati in Azure | Microsoft Docs
description: Viene spiegato il motivo per cui i nomi dei dispositivi sono cambiati e si offre una soluzione a questo problema.
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 789f4580901a22dc3aaae9599c7205c76f268403
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="c22ec-103">Risoluzione dei problemi: nomi dei dispositivi della macchina virtuale Linux modificati</span><span class="sxs-lookup"><span data-stu-id="c22ec-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="c22ec-104">L'articolo spiega i motivi per cui i nomi dei dispositivi sono diversi dopo il riavvio di una macchina virtuale Linux (VM) o dopo aver ricollegato i dischi.</span><span class="sxs-lookup"><span data-stu-id="c22ec-104">The article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach the disks.</span></span> <span data-ttu-id="c22ec-105">offre la soluzione a questo problema.</span><span class="sxs-lookup"><span data-stu-id="c22ec-105">It also provides the solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="c22ec-106">Sintomo</span><span class="sxs-lookup"><span data-stu-id="c22ec-106">Symptom</span></span>

<span data-ttu-id="c22ec-107">È possibile che l'utente debba affrontare i problemi seguenti durante l'esecuzione di macchine virtuali Linux in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c22ec-107">You may experience the following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="c22ec-108">La macchina virtuale non si avvia dopo il riavvio.</span><span class="sxs-lookup"><span data-stu-id="c22ec-108">The VM fails to boot after a restart.</span></span>

- <span data-ttu-id="c22ec-109">Se i dischi di dati vengono scollegati e poi ricollegati, i nomi dei dispositivi per i dischi cambiano.</span><span class="sxs-lookup"><span data-stu-id="c22ec-109">If data disks are detached and reattached, the devices names for disks are changed.</span></span>

- <span data-ttu-id="c22ec-110">Impossibile eseguire un'applicazione o uno script che fa riferimento a un disco con il nome del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c22ec-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="c22ec-111">Ci si accorge che il nome del dispositivo del disco è cambiato.</span><span class="sxs-lookup"><span data-stu-id="c22ec-111">You find that the device name of the disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="c22ec-112">Causa</span><span class="sxs-lookup"><span data-stu-id="c22ec-112">Cause</span></span>

<span data-ttu-id="c22ec-113">La coerenza dei percorsi del dispositivo in Linux non è garantita tra i vari riavvi.</span><span class="sxs-lookup"><span data-stu-id="c22ec-113">Device paths in Linux are not guaranteed to be consistent across restarts.</span></span> <span data-ttu-id="c22ec-114">I nomi del dispositivo sono costituiti da numeri principali, ovvero lettere, e numeri secondari.</span><span class="sxs-lookup"><span data-stu-id="c22ec-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="c22ec-115">Quando il driver del dispositivo di archiviazione di Linux rileva un nuovo dispositivo, assegna un numero di dispositivo principale e secondario dall'intervallo disponibile.</span><span class="sxs-lookup"><span data-stu-id="c22ec-115">When the Linux storage device driver detects a new device, it assigns major and minor device numbers to it from the available range.</span></span> <span data-ttu-id="c22ec-116">Quando un dispositivo viene rimosso, il numero di dispositivi può essere riusato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="c22ec-116">When a device is removed, the device numbers are freed to be reused later.</span></span>

<span data-ttu-id="c22ec-117">Il problema si verifica perché l'analisi del dispositivo in Linux pianificata dal sottosistema SCSI avviene in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="c22ec-117">The problem occurs because the device scanning in Linux scheduled by the SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="c22ec-118">La denominazione del percorso del dispositivo finale può variare tra un riavvio e l'altro.</span><span class="sxs-lookup"><span data-stu-id="c22ec-118">The final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="c22ec-119">Soluzione</span><span class="sxs-lookup"><span data-stu-id="c22ec-119">Solution</span></span>

<span data-ttu-id="c22ec-120">Per risolvere questo problema, usare la denominazione permanente.</span><span class="sxs-lookup"><span data-stu-id="c22ec-120">To resolve this problem, use persistent naming.</span></span> <span data-ttu-id="c22ec-121">Esistono quattro metodi per la denominazione permanente: per etichetta file system, per UUID, per ID e per percorso.</span><span class="sxs-lookup"><span data-stu-id="c22ec-121">There are four methods to persistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="c22ec-122">Per le macchine virtuali Linux di Azure, è consigliabile usare i metodi per etichetta file system e per UUID.</span><span class="sxs-lookup"><span data-stu-id="c22ec-122">We recommend the filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="c22ec-123">La maggior parte delle distribuzioni specifica anche le opzioni fstab **nofail** o **nobootwait**.</span><span class="sxs-lookup"><span data-stu-id="c22ec-123">Most distributions also provide either the **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="c22ec-124">Queste opzioni consentono l'avvio di un sistema anche se il montaggio del disco non riesce in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="c22ec-124">These options enable a system to boot even if the disk fails to mount at startup.</span></span> <span data-ttu-id="c22ec-125">Per altre informazioni su questi parametri, consultare la documentazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c22ec-125">Check the distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="c22ec-126">Per altre informazioni su come configurare una macchina virtuale Linux per l'uso di un UUID quando si aggiunge un disco dati, vedere [Connettersi alla VM Linux per montare il nuovo disco](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="c22ec-126">For more information about how to configure a Linux VM to use a UUID when you add a data disk, see [Connect to the Linux VM to mount the new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="c22ec-127">Quando l'agente Linux di Azure viene installato in una macchina virtuale, questo usa le regole Udev per costruire un set di collegamenti simbolici in **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="c22ec-127">When the Azure Linux agent is installed on a VM, it uses Udev rules to construct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="c22ec-128">Queste regole Udev possono essere usate dalle applicazioni e dagli script per identificare i dischi collegati alla macchina virtuale, il tipo e il LUN.</span><span class="sxs-lookup"><span data-stu-id="c22ec-128">These Udev rules can be used by applications and scripts to identify disks are attached to the VM, their type, and the LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="c22ec-129">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="c22ec-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="c22ec-130">Identificare i LUN del disco</span><span class="sxs-lookup"><span data-stu-id="c22ec-130">Identify disk LUNs</span></span>

<span data-ttu-id="c22ec-131">Un'applicazione può usare i LUN per trovare tutti i dischi collegati e creare i collegamenti simbolici.</span><span class="sxs-lookup"><span data-stu-id="c22ec-131">An application can use LUNs to find all the attached disks and constructing symbolic links.</span></span> <span data-ttu-id="c22ec-132">L'agente Linux di Azure include ora le regole udev che configurano i collegamenti simbolici da un LUN ai dispositivi, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c22ec-132">The Azure Linux agent now includes udev rules that set up symbolic links from a LUN to the devices, as follows:</span></span>

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

<span data-ttu-id="c22ec-133">È possibile recuperare le informazioni sui LUN dal guest Linux con lsscsi o uno strumento simile, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c22ec-133">LUN information can also be retrieved from the Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="c22ec-134">Le informazioni LUN guest possono essere usate con i metadati della sottoscrizione di Azure per identificare la posizione del disco virtuale rigido nell'archivio di Azure che archivia i dati della partizione.</span><span class="sxs-lookup"><span data-stu-id="c22ec-134">This guest LUN information can be used with Azure subscription metadata to identify the location in Azure storage of the VHD which stores the partition data.</span></span> <span data-ttu-id="c22ec-135">Ad esempio, usare az cli:</span><span class="sxs-lookup"><span data-stu-id="c22ec-135">For example, use the az cli:</span></span>

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="c22ec-136">Individuare l'UUID del file system usando blkid</span><span class="sxs-lookup"><span data-stu-id="c22ec-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="c22ec-137">Uno script o un'applicazione possono leggere l'output di blkid oppure fonti di informazioni simili e creare collegamenti simbolici in **/dev**.</span><span class="sxs-lookup"><span data-stu-id="c22ec-137">A script or application can read the output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="c22ec-138">L'output mostra gli UUID di tutti i dischi collegati alla macchina virtuale e il file del dispositivo a cui sono associati:</span><span class="sxs-lookup"><span data-stu-id="c22ec-138">The output will show the UUIDs of all disks attached to the VM and the device file to which they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="c22ec-139">La regola udev waagent crea un set di collegamenti simbolici in **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="c22ec-139">The waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="c22ec-140">L'applicazione può usare queste informazioni identificano il dispositivo del disco di avvio e il disco della risorsa, temporaneo.</span><span class="sxs-lookup"><span data-stu-id="c22ec-140">The application can use this information identify the boot disk device and the resource (ephemeral) disk.</span></span> <span data-ttu-id="c22ec-141">In Azure le applicazioni devono fare riferimento a **/dev/disk/azure/root-part1** o **/dev/disk/azure-resource-part1** per individuare le partizioni.</span><span class="sxs-lookup"><span data-stu-id="c22ec-141">In Azure, applications should refer to **/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** to discover these partitions.</span></span>

<span data-ttu-id="c22ec-142">Se sono presenti partizioni aggiuntive nell'elenco blkid, si trovano in un disco dati.</span><span class="sxs-lookup"><span data-stu-id="c22ec-142">If there are additional partitions from the blkid list, they reside on a data disk.</span></span> <span data-ttu-id="c22ec-143">Le applicazioni possono mantenere l'UUID per tali partizioni e usare un percorso come il seguente per individuare il nome del dispositivo in fase di esecuzione:</span><span class="sxs-lookup"><span data-stu-id="c22ec-143">Applications can maintain the UUID for these partitions and use a path like the below to discover the device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-the-latest-azure-storage-rules"></a><span data-ttu-id="c22ec-144">Ottenere le regole di archiviazione di Azure più recenti</span><span class="sxs-lookup"><span data-stu-id="c22ec-144">Get the latest Azure storage rules</span></span>

<span data-ttu-id="c22ec-145">Per ottenere le regole di archiviazione di Azure più recenti, eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c22ec-145">To the latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="c22ec-146">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="c22ec-146">For more information, see the following articles:</span></span>

- [<span data-ttu-id="c22ec-147">Ubuntu: uso di UUID</span><span class="sxs-lookup"><span data-stu-id="c22ec-147">Ubuntu: Using UUID</span></span>](https://help.ubuntu.com/community/UsingUUID)

- [<span data-ttu-id="c22ec-148">Red Hat: denominazione permanente</span><span class="sxs-lookup"><span data-stu-id="c22ec-148">Red Hat: Persistent Naming</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [<span data-ttu-id="c22ec-149">Linux: operazioni eseguibili con le UUID</span><span class="sxs-lookup"><span data-stu-id="c22ec-149">Linux: What UUIDs can do for you</span></span>](https://www.linux.com/news/what-uuids-can-do-you)

- <span data-ttu-id="c22ec-150">[Udev: Introduction to Device Management In Modern Linux System](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system) (Udev: introduzione alla gestione dei dispositivi nel sistema Linux moderno)</span><span class="sxs-lookup"><span data-stu-id="c22ec-150">[Udev: Introduction to Device Management In Modern Linux System](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)</span></span>

