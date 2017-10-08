---
title: basato su aaaHD economica archiviazione Standard e i dischi di macchina virtuale di Azure | Documenti Microsoft
description: Informazioni sul servizio economicamente conveniente Archiviazione Standard e sui dischi gestiti e non gestiti delle macchine virtuali.
services: storage
documentationcenter: 
author: yuemlu
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: yuemlu
ms.openlocfilehash: c9162eaea50cdd43862378e62dcff9a3d762e092
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cost-effective-standard-storage-and-unmanaged-and-managed-azure-vm-disks"></a>Archiviazione Standard conveniente e dischi gestiti e non gestiti delle macchine virtuali di Azure

Archiviazione Standard di Azure offre un supporto dei dischi affidabile e a basso costo per le VM che eseguono carichi di lavoro non sensibili alla latenza. Supporta anche BLOB, tabelle, code e file. Con l'archiviazione Standard, hello vengono archiviati in unità disco rigido (HDD). Per le VM, è possibile usare dischi di Archiviazione Standard per scenari di sviluppo/test e carichi di lavoro meno critici e dischi di Archiviazione Premium per applicazioni di produzione cruciali. Archiviazione Standard è disponibile in tutte le aree di Azure. 

Questo articolo è incentrato sull'uso di hello dell'archiviazione standard per i dischi di macchina virtuale. Per ulteriori informazioni sull'utilizzo di hello di archiviazione BLOB, tabelle, code e i file, fare riferimento toohello [tooStorage Introduzione](../storage-introduction.md).

## <a name="disk-types"></a>Tipi di disco

Esistono due modi toocreate dischi standard per le macchine virtuali di Azure:

**Non gestita dischi**: si tratta di metodo originali hello in cui si gestiscono hello storage account utilizzati toostore hello disco rigido virtuale i file che corrispondono toohello dischi di macchina virtuale. I file VHD vengono archiviati come BLOB di pagine in account di archiviazione. I dischi non gestiti possono essere collegato tooany dimensioni delle macchine Virtuali di Azure, incluse le VM hello che usano principalmente archiviazione Premium, ad esempio hello DSv2 e serie GS. Macchine virtuali di Azure supportano il collegamento di più dischi standard, consentendo di too256 TB di spazio di archiviazione per ogni macchina virtuale.

[**I dischi di Azure gestiti**](../../virtual-machines/windows/managed-disks-overview.md): questa funzionalità consente di gestire gli account di archiviazione hello usati per i dischi VM hello. Specificare il tipo di hello (Standard o Premium) e le dimensioni del disco è necessario, Azure crea e gestisce disco hello per l'utente. Non è tooworry sull'inserimento di dischi hello tra più account di archiviazione in ordine tooensure che rientrino nei limiti di scalabilità hello per gli account di archiviazione hello - Azure che gestisce automaticamente.

Anche se entrambi i tipi di dischi disponibili, è consigliabile utilizzare le numerose funzionalità sfruttare tootake dischi gestiti.

tooget avviato con l'archiviazione Standard di Azure, visitare [possibile iniziare gratuitamente](https://azure.microsoft.com/pricing/free-trial/). 

Per informazioni su come toocreate una macchina virtuale con dischi gestiti, vedere uno dei seguenti hello articoli.

* [Creare una VM con Resource Manager e PowerShell](/azure/virtual-machines/windows/quick-create-powershell.md)
* [Creare una VM Linux di hello Azure CLI 2.0](../../virtual-machines/windows/quick-create-cli.md)

## <a name="standard-storage-features"></a>Funzionalità di Archiviazione Standard 

Esaminiamo alcune delle funzionalità di hello di archiviazione Standard. Per ulteriori informazioni, vedere [tooAzure introduzione archiviazione](../storage-introduction.md).

**Archiviazione Standard**: Archiviazione Standard di Azure supporta dischi, BLOB, archiviazione di file, tabelle e code di Azure. servizi di archiviazione Standard toouse, iniziare con [creare un account di archiviazione di Azure](storage-create-storage-account.md#create-a-storage-account).

**I dischi di archiviazione standard:** archiviazione Standard possono essere dischi collegati tooall macchine virtuali di Azure tra macchine virtuali di dimensioni della serie utilizzate con archiviazione Premium, ad esempio hello DSv2 e GS serie. Un disco di archiviazione standard può essere collegati tooone macchina virtuale. Tuttavia, è possibile collegare uno o più di questi tooa dischi VM, conteggio massima del disco toohello definito per la dimensione di macchina virtuale. In hello seguendo sezione Standard obiettivi di scalabilità e prestazioni, si descrive le specifiche di hello in modo più dettagliato. 

**Blob di pagine standard**: BLOB di pagine Standard vengono utilizzati toohold dischi persistenti per le macchine virtuali e sono accessibili anche tramite REST, come gli altri tipi di BLOB di Azure. I [BLOB di pagine](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) sono una raccolta di pagine di 512 byte ottimizzata per operazioni di lettura e scrittura casuali. 

**Replica di Archiviazione**: nella maggior parte delle aree, i dati in un account di archiviazione Standard possono essere replicati in locale oppure essere sottoposti a replica geografica tra più data center. Hello quattro tipi di replica disponibile sono archiviazione localmente ridondante (LRS), archiviazione con ridondanza della zona (ZRS), archiviazione con ridondanza geografica (GRS) e archiviazione geograficamente ridondante con accesso in lettura (RA-GRS). In Archiviazione Standard, Managed Disks supporta attualmente solo l'archiviazione con ridondanza locale. Per altre informazioni, vedere [Replica di Archiviazione](../storage-redundancy.md).

## <a name="scalability-and-performance-targets"></a>Obiettivi di scalabilità e prestazioni

In questa sezione si descrive obiettivi di scalabilità e prestazioni di hello è necessario tooconsider quando si utilizza l'archiviazione standard.

### <a name="account-limits--does-not-apply-toomanaged-disks"></a>I limiti dell'account: non si applica toomanaged dischi

| **Risorsa** | **Limite predefinito** |
|--------------|-------------------|
| TB per account di archiviazione  | 500 TB |
| Traffico in ingresso massimo<sup>1</sup> per account di archiviazione (aree degli Stati Uniti) | 10 Gbps con archiviazione GRS/ZRS abilitata, 20 Gbps per LRS |
| Traffico in uscita massimo<sup>1</sup> per account di archiviazione (aree degli Stati Uniti) | 20 Gbps con archiviazione RA-GRS/GRS/ZRS abilitata, 30 Gbps per LRS |
| Traffico in ingresso massimo<sup>1</sup> per account di archiviazione (aree europee e asiatiche) | 5 Gbps con archiviazione GRS/ZRS abilitata, 10 Gbps per LRS |
| Traffico in uscita massimo<sup>1</sup> per account di archiviazione (aree europee e asiatiche) | 10 Gbps con archiviazione RA-GRS/GRS/ZRS abilitata, 15 Gbps per LRS |
| Frequenza di richiesta totale (presupponendo oggetti con dimensione di 1 KB) per account di archiviazione | Backup too20, IOPS 000, entità al secondo o messaggi al secondo |

<sup>1</sup> in ingresso si riferisce a dati tooall (richieste) inviati tooa account di archiviazione. In uscita fa riferimento tooall dati (risposte) ricevuti da un account di archiviazione.

Per altre informazioni, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](../storage-scalability-targets.md).

Se hello deve superare obiettivi di scalabilità hello di un singolo account di archiviazione dell'applicazione, compilare l'applicazione toouse più account di archiviazione e partizionare i dati in tali account di archiviazione. In alternativa, è possibile di dischi gestiti di Azure e Azure gestiscono hello partizionamento e la posizione dei dati per l'utente.

### <a name="standard-disks-limits"></a>Limiti dei dischi Standard

A differenza dei dischi Premium, operazioni di input/output di hello al secondo (IOPS) e la velocità effettiva (larghezza di banda) di dischi Standard non sono disponibile. Hello variazione delle prestazioni dei dischi standard con hello VM dimensioni toowhich hello disco è collegato, non toohello dimensioni del disco di hello. Si può prevedere tooachieve backup limite prestazioni toohello elencati nella tabella hello riportata di seguito.

**Limiti dei dischi Standard (gestiti e non gestiti)**

| **Livello VM**            | **VM livello Basic** | **VM livello Standard** |
|------------------------|-------------------|----------------------|
| Dimensioni massime disco          | 4095 GB           | 4095 GB              |
| Numero massimo di operazioni di I/O al secondo da 8 KB per disco | Backup too300         | Backup too500            |
| Larghezza di banda massima per disco | Backup too60 MB/s     | Backup too60 MB/s        |

Se il carico di lavoro richiede un supporto dei dischi a bassa latenza e prestazioni elevate, è consigliabile valutare la possibilità di usare Archiviazione Premium. tooknow ulteriori vantaggi dell'archiviazione Premium, visitare [archiviazione Premium a prestazioni elevate e dischi di macchina virtuale di Azure](../storage-premium-storage.md). 

## <a name="snapshots-and-copy-blob"></a>Snapshot e copia di BLOB

il servizio di archiviazione, file VHD hello toohello è un blob di pagine. È possibile creare snapshot del BLOB di pagine e copiarli tooanother percorso, ad esempio un account di archiviazione diverso.

### <a name="unmanaged-disks"></a>Dischi non gestiti

È possibile creare [snapshot incrementali](../../virtual-machines/windows/incremental-snapshots.md) per dischi standard non gestito in hello stessa modalità di utilizzo di snapshot con archiviazione Standard. È consigliabile creare gli snapshot e quindi copiare tali account di archiviazione standard con ridondanza geografica tooa snapshot se il disco di origine si trova in un account di archiviazione con ridondanza locale. Per altre informazioni, vedere [Opzioni di ridondanza di Archiviazione di Azure](../storage-redundancy.md).

Se un disco collegato tooa VM, determinate operazioni dell'API non sono consentite nei dischi hello. Ad esempio, non è possibile eseguire un [Copy Blob](/rest/api/storageservices/Copy-Blob) operazione per tale blob purché hello disco è collegato tooa macchina virtuale. In alternativa, è possibile creare innanzitutto uno snapshot del blob utilizzando hello [Snapshot Blob](/rest/api/storageservices/Snapshot-Blob) metodo API REST e quindi eseguire hello [Copy Blob](/rest/api/storageservices/Copy-Blob) di hello toocopy di hello snapshot disco collegato. In alternativa, è possibile scollegare il disco hello e quindi effettuare le operazioni necessarie.

toomaintain copie con ridondanza geografica degli snapshot, è possibile copiare gli snapshot da un account di archiviazione standard con ridondanza geografica tooa di account di archiviazione con ridondanza locale tramite AzCopy o Blob di copia. Per ulteriori informazioni, vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md) e [Copy Blob](/rest/api/storageservices/Copy-Blob).

Per informazioni dettagliate sull'esecuzione di operazioni REST sui BLOB di pagine negli account di archiviazione Standard, vedere l'articolo relativo alle [API REST per i servizi di archiviazione di Azure](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference).

### <a name="managed-disks"></a>Dischi gestiti

Uno snapshot per un disco gestito è una copia di sola lettura del disco hello gestito viene archiviato come un disco gestito standard. Snapshot incrementali non sono attualmente supportati per i dischi gestiti, ma sarà supportato in hello future.

Se un disco gestito è collegato tooa VM, determinate operazioni dell'API non sono consentite nei dischi hello. È ad esempio, non è possibile generare un tooperform di firma di accesso condiviso un'operazione di copia mentre il disco di hello è collegato tooa macchina virtuale. In alternativa, creare innanzitutto uno snapshot del disco hello e quindi eseguire Copia hello dello snapshot hello. In alternativa, è possibile scollegare il disco hello e quindi generare un'operazione di copia hello tooperform firma di accesso condiviso.

## <a name="pricing-and-billing"></a>Prezzi e fatturazione

Quando si utilizza l'archiviazione Standard, hello fatturazione considerazioni seguenti:

* Dimensioni dati/dischi non gestiti di Archiviazione Standard 
* Dischi gestiti Standard
* Snapshot di Archiviazione Standard
* Trasferimenti di dati in uscita
* Transazioni

**Non gestita delle dimensioni dei dati e il disco di archiviazione:** per i dischi non gestiti e altri dati (BLOB, tabelle, code e file), vengono addebitati solo i hello spazio in uso. Ad esempio, se si dispone di una macchina virtuale il cui blob di pagine viene eseguito il provisioning come 127 GB, ma hello macchina virtuale è in realtà solo utilizzando 10 GB di spazio, verrà fatturato per 10 GB di spazio. Un sostegno archiviazione Standard too8191 GB e i dischi non gestiti Standard too4095 GB. 

**Dischi gestiti:** dischi gestiti vengono fatturati dimensione hello il provisioning. Se viene eseguito il provisioning del disco come disco di 10 GB e si usa solo 5 GB, verrà comunque addebitato per le dimensioni di effettuare il provisioning di hello di 10 GB.

**Gli snapshot**: gli snapshot dei dischi standard vengono fatturati per una capacità aggiuntiva hello utilizzata dagli snapshot hello. Per informazioni sugli snapshot, vedere [Creazione di uno snapshot di un BLOB](/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

**Trasferimenti di dati in uscita**: i [trasferimenti di dati in uscita](https://azure.microsoft.com/pricing/details/data-transfers/) (dati in uscita dai data center di Azure) vengono fatturati in base all'uso della larghezza di banda.

**Transazioni**: per Archiviazione Standard, Azure addebita $ 0,0036 per 100.000 transazioni. Le transazioni includono entrambe lettura e scrittura toostorage operazioni.

Per informazioni dettagliate sui prezzi di Archiviazione Standard, Macchine virtuali e Managed Disks, vedere:

* [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/)
* [Prezzi di Macchine virtuali](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Prezzi di Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks)

## <a name="azure-backup-service-support"></a>Supporto del servizio Backup di Azure 

È possibile eseguire il backup delle macchine virtuali con dischi non gestiti con Backup di Azure. [Altre informazioni](../../backup/backup-azure-vms-first-look-arm.md).

È possibile utilizzare anche hello servizio Backup di Azure con dischi gestiti toocreate un processo di backup con backup basate sul tempo, facilmente ripristinati VM e i criteri di conservazione dei backup. Per altre informazioni in merito, vedere la sezione relativa all'[uso del servizio Backup di Azure per macchine virtuali con dischi gestiti](../../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="next-steps"></a>Passaggi successivi

* [Introduzione tooAzure archiviazione](../storage-introduction.md)

* [Creare un account di archiviazione](../storage-create-storage-account.md)

* [Panoramica di Managed Disks](../../virtual-machines/windows/managed-disks-overview.md)

* [Creare una VM con Resource Manager e PowerShell](/azure/virtual-machines/windows/quick-create-powershell.md)

* [Creare una VM Linux di hello Azure CLI 2.0](../../virtual-machines/windows/quick-create-cli.md)
