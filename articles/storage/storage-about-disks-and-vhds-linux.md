---
title: aaaAbout dischi e i dischi rigidi virtuali per le macchine virtuali Linux di Microsoft Azure | Documenti Microsoft
description: Informazioni sui concetti di base di hello di dischi e i dischi rigidi virtuali per le macchine virtuali Linux in Azure.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7be8dd52-98f7-4187-9b78-55197915bc9b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 1155d773136677553d263c17fbf8b224035d96bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a>Informazioni sui dischi e sui dischi rigidi virtuali per le VM Linux di Azure
Analogamente a qualsiasi altro computer, le macchine virtuali in Azure usare dischi come un toostore sul posto del sistema operativo, applicazioni e dati. Tutte le macchine virtuali di Azure dispongono di almeno due dischi: un disco del sistema operativo Linux e un disco temporaneo. disco del sistema operativo Hello è creato da un'immagine disco del sistema operativo hello sia immagine hello sono in realtà dischi rigidi virtuali (VHD) archiviati in un account di archiviazione di Azure. Anche le macchine virtuali possono disporre di uno o più dischi dati archiviati in dischi rigidi virtuali. 

In questo articolo, si parla hello diversi usi dischi hello e quindi illustrano hello diversi tipi di dischi è possibile creare e utilizzare. Questo articolo è disponibile anche per le [macchine virtuali Windows](storage-about-disks-and-vhds-windows.md).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Dischi usati dalle VM

Esaminiamo un utilizzo dischi hello in hello macchine virtuali.

## <a name="operating-system-disk"></a>Disco del sistema operativo
Tutte le macchine virtuali dispongono di un disco del sistema operativo collegato. Per impostazione predefinita, è registrato come unità SATA con etichetta /dev/sda. Questo disco ha una capacità massima di 2048 gigabyte (GB). 

## <a name="temporary-disk"></a>Disco temporaneo
Ogni VM contiene un disco temporaneo. disco temporaneo Hello fornisce l'archiviazione a breve termine per i processi e le applicazioni e dati di archivio tooonly desiderato, ad esempio i file di paging o di scambio. Dati su disco temporaneo hello potrebbero andare persi durante un [evento di manutenzione](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) o quando si [ridistribuire una macchina virtuale](../virtual-machines/linux/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Durante un riavvio standard di hello VM, dati hello nell'unità temporanea hello devono essere rese persistenti.

Nelle macchine virtuali Linux, hello disco è in genere **dev/sdb** formattato e montato troppo**/mnt** da hello agente Linux di Azure. dimensioni Hello del disco temporaneo hello variano in base alle dimensioni di hello della macchina virtuale hello. Per altre informazioni, vedere [Dimensioni per le macchine virtuali Linux](../virtual-machines/linux/sizes.md).

Per ulteriori informazioni sulle modalità di utilizzo disco temporaneo hello Azure, vedere [informazioni sulle unità temporanea hello in macchine virtuali di Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="data-disk"></a>Disco dati
Un disco dati è un disco rigido virtuale collegato tooa macchina virtuale toostore dati dell'applicazione o altri dati necessari tookeep. I dischi dati vengono registrati come unità SCSI ed etichettati con una lettera di propria scelta. Ogni disco dati ha una capacità massima di 4095 GB. dimensione della macchina virtuale hello Hello determina il numero di dischi dati è possibile collegare tooit e hello il tipo di archiviazione è possibile usare dischi hello toohost.

> [!NOTE]
> Per ulteriori dettagli sulle capacità delle macchine virtuali, vedere [Dimensioni per le macchine virtuali Linux](../virtual-machines/linux/sizes.md).
> 

Quando viene creata una macchina virtuale da un'immagine, Azure crea un disco del sistema operativo. Se si utilizza un'immagine che include dischi dati, Azure crea anche hello dischi dati durante la creazione di macchine virtuali hello. In caso contrario, aggiungere dischi dati dopo aver creato una macchina virtuale hello.

È possibile aggiungere da macchina virtuale tooa dischi di dati in qualsiasi momento, **collegamento** hello macchina virtuale di toohello disco. È possibile utilizzare un disco rigido virtuale che è stato caricato o copiato tooyour account di archiviazione o uno che Azure crea automaticamente. Collegando un disco dati associa file di disco rigido virtuale hello hello VM, inserendo un 'lease' sul disco rigido virtuale hello pertanto non può essere eliminato dall'archiviazione mentre è ancora collegato.

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a>Risoluzione dei problemi
[!INCLUDE [virtual-machines-linux-lunzero](../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Passaggi successivi
* [Collegare un disco](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooadd ulteriore spazio di archiviazione per la macchina virtuale.
* [Configurare RAID software](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per la ridondanza.
* [Acquisire una macchina virtuale Linux](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) per poter distribuire rapidamente macchine virtuali aggiuntive.

