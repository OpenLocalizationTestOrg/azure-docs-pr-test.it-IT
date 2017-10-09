---
title: aaaAbout dischi e i dischi rigidi virtuali per macchine virtuali di Windows di Microsoft Azure | Documenti Microsoft
description: Informazioni sui concetti di base di hello di dischi e i dischi rigidi virtuali per Windows macchine virtuali in Azure.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 859e564dc74240bd7c70fec33255b8d071c4acf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a>Informazioni sui dischi e sui dischi rigidi virtuali per le VM Windows di Azure
Analogamente a qualsiasi altro computer, le macchine virtuali in Azure usare dischi come un toostore sul posto del sistema operativo, applicazioni e dati. Tutte le macchine virtuali di Azure dispongono di almeno due dischi: un disco del sistema operativo Windows e un disco temporaneo. disco del sistema operativo Hello è creato da un'immagine disco del sistema operativo hello sia immagine hello sono dischi rigidi virtuali (VHD) archiviati in un account di archiviazione di Azure. Anche le macchine virtuali possono disporre di uno o più dischi dati archiviati in dischi rigidi virtuali. 

In questo articolo, si parla hello diversi usi dischi hello e quindi illustrano hello diversi tipi di dischi è possibile creare e utilizzare. Questo articolo è disponibile anche per le [macchine virtuali Linux](storage-about-disks-and-vhds-linux.md).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Dischi usati dalle VM

Esaminiamo un utilizzo dischi hello in hello macchine virtuali.

### <a name="operating-system-disk"></a>Disco del sistema operativo
Tutte le macchine virtuali dispongono di un disco del sistema operativo collegato. Ha registrato come unità SATA ed etichettato come unità c: hello per impostazione predefinita. Questo disco ha una capacità massima di 2048 GB. 

### <a name="temporary-disk"></a>Disco temporaneo
Ogni VM contiene un disco temporaneo. disco temporaneo Hello fornisce l'archiviazione a breve termine per i processi e le applicazioni e dati di archivio tooonly desiderato, ad esempio i file di paging o di scambio. Dati su disco temporaneo hello potrebbero andare persi durante un [evento di manutenzione](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) o quando si [ridistribuire una macchina virtuale](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Durante un riavvio standard di hello VM, dati hello nell'unità temporanea hello devono essere rese persistenti.

disco temporaneo Hello viene etichettato come unità d: hello, per impostazione predefinita e viene utilizzato per l'archiviazione pagefile.sys. tooremap questa lettera di unità diversa tooa disco, vedere [lettera di unità di modifica hello del disco temporaneo di Windows hello](../virtual-machines/windows/change-drive-letter.md). dimensioni Hello del disco temporaneo hello variano in base alle dimensioni di hello della macchina virtuale hello. Per maggiori informazioni, vedere [Dimensioni delle macchine virtuali di Windows](../virtual-machines/windows/sizes.md).

Per ulteriori informazioni sulle modalità di utilizzo disco temporaneo hello Azure, vedere [informazioni sulle unità temporanea hello in macchine virtuali di Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)


### <a name="data-disk"></a>Disco dati
Un disco dati è un disco rigido virtuale collegato tooa macchina virtuale toostore dati dell'applicazione o altri dati necessari tookeep. I dischi dati vengono registrati come unità SCSI ed etichettati con una lettera di propria scelta. Ogni disco dati ha una capacità massima di 4095 GB. dimensione della macchina virtuale hello Hello determina il numero di dischi dati è possibile collegare tooit e hello il tipo di archiviazione è possibile usare dischi hello toohost.

> [!NOTE]
> Per altre informazioni sulle capacità delle macchine virtuali, vedere [Dimensioni delle macchine virtuali di Windows](../virtual-machines/windows/sizes.md).
> 

Quando viene creata una macchina virtuale da un'immagine, Azure crea un disco del sistema operativo. Se si utilizza un'immagine che include dischi dati, Azure crea anche hello dischi dati durante la creazione di macchine virtuali hello. In caso contrario, aggiungere dischi dati dopo aver creato una macchina virtuale hello.

È possibile aggiungere da macchina virtuale tooa dischi di dati in qualsiasi momento, **collegamento** hello macchina virtuale di toohello disco. È possibile utilizzare un disco rigido virtuale che è stato caricato o copiato tooyour account di archiviazione o uno che Azure crea automaticamente. Collegando un disco dati associa file di disco rigido virtuale hello hello VM inserendo un 'lease' sul disco rigido virtuale hello pertanto non può essere eliminato dall'archiviazione mentre è ancora collegato.


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a>Un ultimo suggerimento: usare TRIM con i dischi standard non gestiti 

Se si usano dischi standard non gestiti, è consigliabile abilitare TRIM. TRIM rimuove i blocchi inutilizzati nel disco hello in modo verrà addebitato solo per l'archiviazione che stiano effettivamente usando. In questo modo è possibile risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli. 

È possibile eseguire questo comando toocheck hello TRIM impostare. Aprire un prompt dei comandi nella macchina virtuale Windows e digitare:


```
fsutil behavior query DisableDeleteNotify
```

Se il comando hello restituisce 0, l'ottimizzazione TRIM è abilitato correttamente. Se viene restituito 1, eseguire hello tooenable comando TRIM seguenti:

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> Nota: Il supporto dell'ottimizzazione inizia con Windows Server 2012 o Windows 8 e versioni successive, vedere vedere [nuova API consente alle App media toostorage di hint "TRIM e annullare il mapping di" toosend](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a>Passaggi successivi
* [Collegare un disco](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd ulteriore spazio di archiviazione per la macchina virtuale.
* [Lettera di unità di modifica hello del disco temporaneo di Windows hello](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) affinché l'applicazione può utilizzare l'unità d: hello per i dati.

