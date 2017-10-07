---
title: vengono modificati i nomi dei dispositivi di aaaLinux macchina virtuale in Azure | Documenti Microsoft
description: "Illustra hello perché vengono modificati i nomi dei dispositivi e fornire soluzioni per questo problema."
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
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="57e44-103">Risoluzione dei problemi: nomi dei dispositivi della macchina virtuale Linux modificati</span><span class="sxs-lookup"><span data-stu-id="57e44-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="57e44-104">articolo Hello spiega perché i nomi dei dispositivi vengano modificati dopo il riavvio di una macchina virtuale Linux (VM) o ricollegare dischi hello.</span><span class="sxs-lookup"><span data-stu-id="57e44-104">hello article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach hello disks.</span></span> <span data-ttu-id="57e44-105">Fornisce inoltre una soluzione di hello per questo problema.</span><span class="sxs-lookup"><span data-stu-id="57e44-105">It also provides hello solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="57e44-106">Sintomo</span><span class="sxs-lookup"><span data-stu-id="57e44-106">Symptom</span></span>

<span data-ttu-id="57e44-107">Potrebbero verificarsi hello seguenti problemi durante l'esecuzione di macchine virtuali Linux in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="57e44-107">You may experience hello following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="57e44-108">Hello macchina virtuale non riesce tooboot dopo un riavvio.</span><span class="sxs-lookup"><span data-stu-id="57e44-108">hello VM fails tooboot after a restart.</span></span>

- <span data-ttu-id="57e44-109">Se i dischi dati sono scollegare e ricollegare, vengono modificati i nomi di dispositivi hello per i dischi.</span><span class="sxs-lookup"><span data-stu-id="57e44-109">If data disks are detached and reattached, hello devices names for disks are changed.</span></span>

- <span data-ttu-id="57e44-110">Impossibile eseguire un'applicazione o uno script che fa riferimento a un disco con il nome del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="57e44-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="57e44-111">Trovare tale hello Nome dispositivo del disco hello viene modificato.</span><span class="sxs-lookup"><span data-stu-id="57e44-111">You find that hello device name of hello disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="57e44-112">Causa</span><span class="sxs-lookup"><span data-stu-id="57e44-112">Cause</span></span>

<span data-ttu-id="57e44-113">I percorsi di dispositivo in Linux non sono garantiti toobe coerente tra i vari riavvi.</span><span class="sxs-lookup"><span data-stu-id="57e44-113">Device paths in Linux are not guaranteed toobe consistent across restarts.</span></span> <span data-ttu-id="57e44-114">I nomi del dispositivo sono costituiti da numeri principali, ovvero lettere, e numeri secondari.</span><span class="sxs-lookup"><span data-stu-id="57e44-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="57e44-115">Quando i driver di dispositivo di archiviazione Linux hello rileva un nuovo dispositivo, assegna tooit numeri dispositivo principale e secondaria dall'intervallo di hello disponibili.</span><span class="sxs-lookup"><span data-stu-id="57e44-115">When hello Linux storage device driver detects a new device, it assigns major and minor device numbers tooit from hello available range.</span></span> <span data-ttu-id="57e44-116">Quando un dispositivo viene rimosso, i numeri di periferica hello sono toobe liberato riutilizzato in seguito.</span><span class="sxs-lookup"><span data-stu-id="57e44-116">When a device is removed, hello device numbers are freed toobe reused later.</span></span>

<span data-ttu-id="57e44-117">Hello problema si verifica perché hello dispositivo l'analisi in Linux pianificata dal sottosistema SCSI hello avviene in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="57e44-117">hello problem occurs because hello device scanning in Linux scheduled by hello SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="57e44-118">denominazione di Hello dispositivo finale percorso può variare tra i vari riavvi.</span><span class="sxs-lookup"><span data-stu-id="57e44-118">hello final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="57e44-119">Soluzione</span><span class="sxs-lookup"><span data-stu-id="57e44-119">Solution</span></span>

<span data-ttu-id="57e44-120">tooresolve questo problema, utilizzare nomi permanente.</span><span class="sxs-lookup"><span data-stu-id="57e44-120">tooresolve this problem, use persistent naming.</span></span> <span data-ttu-id="57e44-121">Esistono quattro metodi toopersistent denominazione - tramite etichetta filesystem, uuid, dall'id e dal percorso.</span><span class="sxs-lookup"><span data-stu-id="57e44-121">There are four methods toopersistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="57e44-122">È consigliabile etichetta filesystem hello e metodi UUID per le macchine virtuali Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="57e44-122">We recommend hello filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="57e44-123">La maggior parte delle distribuzioni anche forniscono entrambi hello **nofail** o **nobootwait** fstab opzioni.</span><span class="sxs-lookup"><span data-stu-id="57e44-123">Most distributions also provide either hello **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="57e44-124">Queste opzioni consentono un tooboot sistema anche se l'errore del disco contenente hello toomount all'avvio.</span><span class="sxs-lookup"><span data-stu-id="57e44-124">These options enable a system tooboot even if hello disk fails toomount at startup.</span></span> <span data-ttu-id="57e44-125">Consultare la documentazione della distribuzione hello per ulteriori informazioni su questi parametri.</span><span class="sxs-lookup"><span data-stu-id="57e44-125">Check hello distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="57e44-126">Per ulteriori informazioni su come tooconfigure toouse una VM Linux un UUID quando si aggiunge un disco dati, vedere [connettersi toohello nuovo disco VM Linux toomount hello](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="57e44-126">For more information about how tooconfigure a Linux VM toouse a UUID when you add a data disk, see [Connect toohello Linux VM toomount hello new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="57e44-127">Quando l'agente Linux di Azure hello viene installato in una macchina virtuale, viene utilizzato Udev regole tooconstruct un set di collegamenti simbolici in **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="57e44-127">When hello Azure Linux agent is installed on a VM, it uses Udev rules tooconstruct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="57e44-128">Queste regole Udev possono essere usate dalle applicazioni e i dischi tooidentify gli script sono collegato toohello macchina virtuale, al tipo e hello LUN.</span><span class="sxs-lookup"><span data-stu-id="57e44-128">These Udev rules can be used by applications and scripts tooidentify disks are attached toohello VM, their type, and hello LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="57e44-129">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="57e44-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="57e44-130">Identificare i LUN del disco</span><span class="sxs-lookup"><span data-stu-id="57e44-130">Identify disk LUNs</span></span>

<span data-ttu-id="57e44-131">Un'applicazione può utilizzare LUN toofind tutti i dischi collegato hello e si creano i collegamenti simbolici.</span><span class="sxs-lookup"><span data-stu-id="57e44-131">An application can use LUNs toofind all hello attached disks and constructing symbolic links.</span></span> <span data-ttu-id="57e44-132">l'agente Linux di Azure Hello ora include regole udev configurare i collegamenti simbolici dai dispositivi toohello LUN, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="57e44-132">hello Azure Linux agent now includes udev rules that set up symbolic links from a LUN toohello devices, as follows:</span></span>

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
                                 

<span data-ttu-id="57e44-133">Possono inoltre recuperare informazioni di LUN Guest Linux hello utilizzando lsscsi o uno strumento simile nel modo seguente.</span><span class="sxs-lookup"><span data-stu-id="57e44-133">LUN information can also be retrieved from hello Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="57e44-134">Le informazioni LUN guest è utilizzabile con sottoscrizione di Azure metadati tooidentify hello percorso nell'archiviazione di Azure del VHD che archivia i dati di partizione hello hello.</span><span class="sxs-lookup"><span data-stu-id="57e44-134">This guest LUN information can be used with Azure subscription metadata tooidentify hello location in Azure storage of hello VHD which stores hello partition data.</span></span> <span data-ttu-id="57e44-135">Ad esempio, utilizzare hello az cli:</span><span class="sxs-lookup"><span data-stu-id="57e44-135">For example, use hello az cli:</span></span>

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="57e44-136">Individuare l'UUID del file system usando blkid</span><span class="sxs-lookup"><span data-stu-id="57e44-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="57e44-137">Uno script o l'applicazione può leggere l'output di hello di ID blocco o simile fonti di informazioni e creare collegamenti simbolici in **/dev** per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="57e44-137">A script or application can read hello output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="57e44-138">Mostra output di Hello hello UUID di tutti i dischi collegati toohello macchina virtuale e hello dispositivo file toowhich sono associate:</span><span class="sxs-lookup"><span data-stu-id="57e44-138">hello output will show hello UUIDs of all disks attached toohello VM and hello device file toowhich they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="57e44-139">le regole di Hello waagent udev costruire un set di collegamenti simbolici in **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="57e44-139">hello waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="57e44-140">un'applicazione Hello è possibile utilizzare queste informazioni identificano dispositivo disco di avvio hello e il disco di risorsa (temporaneo) hello.</span><span class="sxs-lookup"><span data-stu-id="57e44-140">hello application can use this information identify hello boot disk device and hello resource (ephemeral) disk.</span></span> <span data-ttu-id="57e44-141">In Azure, devono fare riferimento troppo applicazioni**/dev/disk/azure/root-part1** o **/dev/disk/azure-resource-part1** toodiscover tali partizioni.</span><span class="sxs-lookup"><span data-stu-id="57e44-141">In Azure, applications should refer too**/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** toodiscover these partitions.</span></span>

<span data-ttu-id="57e44-142">Se sono presenti altre partizioni dall'elenco di ID blocco hello, si trovano in un disco dati.</span><span class="sxs-lookup"><span data-stu-id="57e44-142">If there are additional partitions from hello blkid list, they reside on a data disk.</span></span> <span data-ttu-id="57e44-143">Applicazioni di gestire hello UUID per tali partizioni e utilizzare un percorso come hello sotto il nome di dispositivo toodiscover hello in fase di esecuzione:</span><span class="sxs-lookup"><span data-stu-id="57e44-143">Applications can maintain hello UUID for these partitions and use a path like hello below toodiscover hello device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a><span data-ttu-id="57e44-144">Ottenere le regole di archiviazione di Azure più recenti hello</span><span class="sxs-lookup"><span data-stu-id="57e44-144">Get hello latest Azure storage rules</span></span>

<span data-ttu-id="57e44-145">toohello regole di archiviazione di Azure più recenti, eseguire il seguente comandi:</span><span class="sxs-lookup"><span data-stu-id="57e44-145">toohello latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="57e44-146">Per ulteriori informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="57e44-146">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="57e44-147">Ubuntu: uso di UUID</span><span class="sxs-lookup"><span data-stu-id="57e44-147">Ubuntu: Using UUID</span></span>](https://help.ubuntu.com/community/UsingUUID)

- [<span data-ttu-id="57e44-148">Red Hat: denominazione permanente</span><span class="sxs-lookup"><span data-stu-id="57e44-148">Red Hat: Persistent Naming</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [<span data-ttu-id="57e44-149">Linux: operazioni eseguibili con le UUID</span><span class="sxs-lookup"><span data-stu-id="57e44-149">Linux: What UUIDs can do for you</span></span>](https://www.linux.com/news/what-uuids-can-do-you)

- [<span data-ttu-id="57e44-150">Udev: Introduzione tooDevice Management nel sistema Linux moderna</span><span class="sxs-lookup"><span data-stu-id="57e44-150">Udev: Introduction tooDevice Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

