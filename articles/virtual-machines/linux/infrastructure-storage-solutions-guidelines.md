---
title: soluzioni aaaStorage per le macchine virtuali Linux in Azure | Documenti Microsoft
description: Informazioni su hello progettazione e implementazione di linee guida fondamentali per la distribuzione di soluzioni di archiviazione in servizi di infrastruttura di Azure.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3c368f07-189b-4520-bbe2-f4080253bbf2
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d270c4786d7b55b18b011aa345063b6816a80876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-linux-vms"></a>Linee guida per l'infrastruttura di archiviazione di Azure per macchine virtuali Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Questo articolo è incentrato sulla comprensione delle esigenze di archiviazione e sulle considerazioni di progettazione per il raggiungimento di livelli di prestazioni ottimali delle macchine virtuali (VM).

## <a name="implementation-guidelines-for-storage"></a>Linee guida di implementazione per l'archiviazione
Decisioni:

* Verranno toouse dischi gestiti di Azure o i dischi non gestiti?
* È necessario spazio di archiviazione toouse Standard o Premium per il carico di lavoro?
* È necessario dischi toocreate lo striping di disco più di 4TB?
* È necessario lo striping tooachieve ottimale i/o del disco per il carico di lavoro?
* Il set di account di archiviazione è necessario toohost l'infrastruttura o il carico di lavoro IT?

Attività:

* Rivedere le richieste dei / o delle applicazioni di hello si distribuiscono e si prevede di tipo di account di archiviazione e il numero appropriato di hello.
* Creare set di hello di account di archiviazione usando la convenzione di denominazione. È possibile utilizzare il portale di Azure CLI o hello hello.

## <a name="storage"></a>Archiviazione
Archiviazione di Azure è una parte fondamentale della distribuzione e della gestione di applicazioni e macchine virtuali. Archiviazione di Azure fornisce servizi per l'archiviazione dei dati dei file, dati non strutturati e i messaggi e fa anche parte dell'infrastruttura di hello che supporta le macchine virtuali.

[I dischi di Azure gestiti](../../storage/storage-managed-disks-overview.md) gestisce l'archiviazione dei background hello. Con i dischi non gestiti, per creare gli account di archiviazione dischi hello toohold (file VHD) per le macchine virtuali di Azure. La scalabilità, è necessario assicurarsi creato gli account di archiviazione aggiuntivo in modo da non superare il limite di IOPS hello per l'archiviazione con uno qualsiasi dei dischi. Con dischi gestiti gestione archiviazione, non è limitato da hello limiti dell'account di archiviazione (ad esempio 20.000 IOPS / account). Inoltre non è più necessario toocopy gli account di archiviazione toomultiple immagini personalizzate (file VHD). È possibile gestirli in una posizione centrale: un account di archiviazione per ogni area di Azure e usarli toocreate centinaia di macchine virtuali in una sottoscrizione. È consigliabile usare Managed Disks per le nuove distribuzioni.

Per il supporto delle macchine virtuali sono disponibili due tipi di archiviazione:

* Consentono di account di archiviazione standard accedere archiviazione tooblob (utilizzato per l'archiviazione dei dischi di macchina virtuale di Azure), archiviazione, l'archiviazione delle code, tabelle e file di archiviazione.
* [Archiviazione Premium](../../storage/storage-premium-storage.md) offre prestazioni elevate e supporto per dischi a bassa latenza per carichi di lavoro con uso intensivo di I/O, ad esempio cluster condivisi MongoDB. Attualmente l'archiviazione Premium di Azure supporta solo i dischi di VM di Azure.

Azure consente di creare macchine virtuali con un disco del sistema operativo, un disco temporaneo e nessuno o più dischi dati facoltativi. disco del sistema operativo Hello e i dischi dati sono BLOB di pagine di Azure, mentre il disco temporaneo hello archiviato localmente nel nodo hello in cui risiede la macchina hello. Prestare attenzione quando si progettano applicazioni tooonly utilizzano il disco temporaneo per i dati non persistenti come hello VM può eseguire la migrazione tra host durante un evento di manutenzione. Tutti i dati archiviati su disco temporaneo hello potrebbero essere persi.

Durabilità e disponibilità elevata viene fornito da hello sottostante tooensure ambiente di archiviazione di Azure che i dati rimangono protetti in caso di errori hardware o di manutenzione non pianificata. Quando si progetta l'ambiente di archiviazione di Azure, è possibile scegliere l'archiviazione macchina virtuale tooreplicate:

* in locale all'interno di un data center di Azure
* nei vari data center di Azure all'interno di una determinata area;
* nei vari data center di Azure all'interno di aree diverse.

È possibile leggere [ulteriori informazioni sulle opzioni di replica hello per la disponibilità elevata](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).

I dischi dati e del sistema operativo hanno una dimensione massima di 4TB. È possibile utilizzare questo limite logico Volume Manager (LVM) toosurpass dal pool di dischi toopresent logico volumi di dati maggiori di 1023GB tooyour VM insieme.

Quando si progettano le distribuzioni di Archiviazione di Azure, esistono alcuni limiti di scalabilità. Per altre informazioni, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../../azure-subscription-service-limits.md#storage-limits). Vedere anche [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](../../storage/storage-scalability-targets.md).

Quanto all'archiviazione delle applicazioni, è possibile archiviare dati oggetto non strutturati, ad esempio documenti, immagini, backup, dati di configurazione, log e così via usando l'archiviazione BLOB. Anziché l'applicazione scrittura tooa disco virtuale collegato toohello VM, un'applicazione hello possibile scrivere direttamente nell'archiviazione blob tooAzure. Archiviazione BLOB offre inoltre l'opzione di hello di [a caldo e interessanti livelli di archiviazione](../../storage/storage-blob-storage-tiers.md) in base alle esigenze di disponibilità e i vincoli di costo.

## <a name="striped-disks"></a>Dischi con striping
Oltre a consentire dischi toocreate maggiore di 1023 GB, in molti casi, utilizzare lo striping dei dischi dati migliora le prestazioni, consentendo più BLOB di archiviazione hello tooback per un singolo volume. Con lo striping hello i/o necessari toowrite e lettura dei dati da un singolo disco logico consente di passare in parallelo.

Azure impone limiti sul numero hello di dischi dati e la quantità di larghezza di banda disponibile, a seconda delle dimensioni della macchina virtuale hello. Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md)

Se si utilizza lo striping del disco per i dischi di dati di Azure, è consigliabile hello alle linee guida:

* Collegare i dischi di dati massimo hello consentiti per hello dimensioni della macchina virtuale.
* Usare la gestione dei volumi logici (LVM).
* Evitare di usare le opzioni di memorizzazione nella cache del disco di dati di Azure (criterio di memorizzazione nella cache = Nessuno).

Per ulteriori informazioni, vedere [Configurare LVM in una macchina virtuale Linux](configure-lvm.md).

## <a name="multiple-storage-accounts"></a>Account di archiviazione multipli
In questa sezione non si applica troppo[dischi gestiti di Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), come non creare gli account di archiviazione separata. 

Quando si progetta l'ambiente di archiviazione di Azure per i dischi non gestiti, è possibile utilizzare più account di archiviazione come il numero di hello di macchine virtuali distribuiti aumenta. Questo approccio consente di distribuire out hello i/o tra hello sottostante servizio di archiviazione Azure infrastruttura toomaintain prestazioni ottimali per le macchine virtuali e applicazioni. Durante la Progettazione applicazioni hello che si desidera distribuire, considerare i requisiti dei / o hello che ogni macchina virtuale dispone e saldo out tali macchine virtuali tra account di archiviazione di Azure. Provare a tooavoid raggruppamento tutti hello i/o richiedono le macchine virtuali negli account di archiviazione toojust uno o due.

Per ulteriori informazioni sulle funzionalità dei / o hello le diverse opzioni di archiviazione di Azure hello e per consigliare valori massimi, vedere [obiettivi di scalabilità e prestazioni di archiviazione di Azure](../../storage/storage-scalability-targets.md).

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

