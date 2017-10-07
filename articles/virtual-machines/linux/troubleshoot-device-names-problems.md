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
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>Risoluzione dei problemi: nomi dei dispositivi della macchina virtuale Linux modificati

articolo Hello spiega perché i nomi dei dispositivi vengano modificati dopo il riavvio di una macchina virtuale Linux (VM) o ricollegare dischi hello. Fornisce inoltre una soluzione di hello per questo problema.

## <a name="symptom"></a>Sintomo

Potrebbero verificarsi hello seguenti problemi durante l'esecuzione di macchine virtuali Linux in Microsoft Azure.

- Hello macchina virtuale non riesce tooboot dopo un riavvio.

- Se i dischi dati sono scollegare e ricollegare, vengono modificati i nomi di dispositivi hello per i dischi.

- Impossibile eseguire un'applicazione o uno script che fa riferimento a un disco con il nome del dispositivo. Trovare tale hello Nome dispositivo del disco hello viene modificato.

## <a name="cause"></a>Causa

I percorsi di dispositivo in Linux non sono garantiti toobe coerente tra i vari riavvi. I nomi del dispositivo sono costituiti da numeri principali, ovvero lettere, e numeri secondari.  Quando i driver di dispositivo di archiviazione Linux hello rileva un nuovo dispositivo, assegna tooit numeri dispositivo principale e secondaria dall'intervallo di hello disponibili. Quando un dispositivo viene rimosso, i numeri di periferica hello sono toobe liberato riutilizzato in seguito.

Hello problema si verifica perché hello dispositivo l'analisi in Linux pianificata dal sottosistema SCSI hello avviene in modo asincrono. denominazione di Hello dispositivo finale percorso può variare tra i vari riavvi. 

## <a name="solution"></a>Soluzione

tooresolve questo problema, utilizzare nomi permanente. Esistono quattro metodi toopersistent denominazione - tramite etichetta filesystem, uuid, dall'id e dal percorso. È consigliabile etichetta filesystem hello e metodi UUID per le macchine virtuali Linux di Azure. 

La maggior parte delle distribuzioni anche forniscono entrambi hello **nofail** o **nobootwait** fstab opzioni. Queste opzioni consentono un tooboot sistema anche se l'errore del disco contenente hello toomount all'avvio. Consultare la documentazione della distribuzione hello per ulteriori informazioni su questi parametri. Per ulteriori informazioni su come tooconfigure toouse una VM Linux un UUID quando si aggiunge un disco dati, vedere [connettersi toohello nuovo disco VM Linux toomount hello](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk). 

Quando l'agente Linux di Azure hello viene installato in una macchina virtuale, viene utilizzato Udev regole tooconstruct un set di collegamenti simbolici in **/dev/disk/azure**. Queste regole Udev possono essere usate dalle applicazioni e i dischi tooidentify gli script sono collegato toohello macchina virtuale, al tipo e hello LUN.

## <a name="more-information"></a>Altre informazioni

### <a name="identify-disk-luns"></a>Identificare i LUN del disco

Un'applicazione può utilizzare LUN toofind tutti i dischi collegato hello e si creano i collegamenti simbolici. l'agente Linux di Azure Hello ora include regole udev configurare i collegamenti simbolici dai dispositivi toohello LUN, come indicato di seguito:

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
                                 

Possono inoltre recuperare informazioni di LUN Guest Linux hello utilizzando lsscsi o uno strumento simile nel modo seguente.

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

Le informazioni LUN guest è utilizzabile con sottoscrizione di Azure metadati tooidentify hello percorso nell'archiviazione di Azure del VHD che archivia i dati di partizione hello hello. Ad esempio, utilizzare hello az cli:

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a>Individuare l'UUID del file system usando blkid

Uno script o l'applicazione può leggere l'output di hello di ID blocco o simile fonti di informazioni e creare collegamenti simbolici in **/dev** per l'utilizzo. Mostra output di Hello hello UUID di tutti i dischi collegati toohello macchina virtuale e hello dispositivo file toowhich sono associate:

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

le regole di Hello waagent udev costruire un set di collegamenti simbolici in **/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


un'applicazione Hello è possibile utilizzare queste informazioni identificano dispositivo disco di avvio hello e il disco di risorsa (temporaneo) hello. In Azure, devono fare riferimento troppo applicazioni**/dev/disk/azure/root-part1** o **/dev/disk/azure-resource-part1** toodiscover tali partizioni.

Se sono presenti altre partizioni dall'elenco di ID blocco hello, si trovano in un disco dati. Applicazioni di gestire hello UUID per tali partizioni e utilizzare un percorso come hello sotto il nome di dispositivo toodiscover hello in fase di esecuzione:

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a>Ottenere le regole di archiviazione di Azure più recenti hello

toohello regole di archiviazione di Azure più recenti, eseguire il seguente comandi:

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


Per ulteriori informazioni, vedere hello seguenti articoli:

- [Ubuntu: uso di UUID](https://help.ubuntu.com/community/UsingUUID)

- [Red Hat: denominazione permanente](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [Linux: operazioni eseguibili con le UUID](https://www.linux.com/news/what-uuids-can-do-you)

- [Udev: Introduzione tooDevice Management nel sistema Linux moderna](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

