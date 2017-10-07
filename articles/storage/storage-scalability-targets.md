---
title: "aaaAzure obiettivi di scalabilità e prestazioni | Documenti Microsoft"
description: "Informazioni sulle destinazioni di scalabilità e prestazioni hello per l'archiviazione di Azure, tra cui capacità, velocità di richiesta e della larghezza di banda in ingresso e in uscita per entrambi gli account di archiviazione standard e premium. Comprendere obiettivi di prestazioni per le partizioni all'interno di ognuno dei servizi di archiviazione di Azure hello."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: 98de116a01b64f3418808a5f626b6c70d8d432e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Obiettivi di scalabilità e prestazioni per Archiviazione di Azure
## <a name="overview"></a>Panoramica
In questo argomento vengono descritti argomenti di scalabilità e prestazioni di hello per archiviazione di Microsoft Azure. Per un riepilogo degli altri limiti di Azure, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).

> [!NOTE]
> Tutti gli account di archiviazione eseguiti sulla nuova topologia di rete lineare hello e supportano obiettivi di scalabilità e prestazioni di hello indicati di seguito, indipendentemente dal momento in cui sono stati creati. Per ulteriori informazioni sull'architettura di rete lineare di archiviazione di Azure hello e sulla scalabilità, vedere [archiviazione di Microsoft Azure: A elevata disponibilità servizio di archiviazione Cloud con verifica coerenza sicuro](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).
> 
> [!IMPORTANT]
> obiettivi di scalabilità e prestazioni di Hello elencati di seguito sono di fascia alta, ma possono comunque essere raggiunti. In tutti i casi, la richiesta di hello velocità e larghezza di banda ottenuto dall'account di archiviazione dipende dalle dimensioni hello degli oggetti archiviati, criteri di accesso hello utilizzate e tipo di carico di lavoro che esegue l'applicazione hello. Essere tootest che il servizio toodetermine se le relative prestazioni soddisfano i requisiti. Se possibile, evitare picchi improvvisi nella frequenza di hello del traffico e verificare che il traffico sia ben distribuito tra partizioni.
> 
> Quando l'applicazione raggiunge il limite di hello di ciò che è possibile gestire una partizione per il carico di lavoro, archiviazione di Azure inizierà tooreturn codice di errore 503 (Server occupato) o codice di errore 500 risposte (Timeout operazione). In questo caso, un'applicazione hello debba utilizzare criteri di backoff esponenziale per i tentativi. backoff esponenziale Hello consente carico hello hello partizione toodecrease e tooease out picchi nella partizione toothat traffico.
> 
> 

Dell'applicazione hello deve superare obiettivi di scalabilità hello di un singolo account di archiviazione, è possibile compilare l'applicazione toouse più account di archiviazione e il partizionamento di oggetti dati in tali account di archiviazione. Per informazioni sui prezzi in base al volume, vedere la pagina relativa ai [prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/) .

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>Obiettivi di scalabilità per BLOB, code, tabelle e file
[!INCLUDE [azure-storage-limits](../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a>Obiettivi di scalabilità per i dischi della macchina virtuale
[!INCLUDE [azure-storage-limits-vm-disks](../../includes/azure-storage-limits-vm-disks.md)]

Per altri dettagli, vedere [Dimensioni per le macchine virtuali Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [Dimensioni per le macchine virtuali Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="managed-virtual-machine-disks"></a>Dischi delle macchine virtuali gestiti

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a>Dischi delle macchine virtuali non gestiti
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a>Obiettivi di scalabilità per Gestione risorse di Azure
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a>Partizioni in Archiviazione di Azure
Ogni oggetto che contiene i dati archiviati in archiviazione di Azure (BLOB, messaggi, le entità e file) appartiene la partizione tooa ed è identificato da una chiave di partizione. partizione Hello determina la modalità di archiviazione di Azure bilancia il carico BLOB, messaggi, le entità e i file tra requisiti di tali oggetti server toomeet hello traffico. chiave di partizione Hello è univoca ed è utilizzato toolocate un blob, un messaggio o l'entità.

tabella Hello illustrata in precedenza [obiettivi di scalabilità per gli account di archiviazione Standard](#standard-storage-accounts) elenchi hello obiettivi di prestazioni per una singola partizione per ogni servizio.

Le partizioni influiscono sul bilanciamento del carico e scalabilità per ognuno dei servizi di archiviazione hello in hello seguenti modi:

* **BLOB**: chiave di partizione hello per un blob è il nome di account + nome contenitore + nome blob. Ciò significa che ogni blob può avere una propria partizione se il carico sul blob hello lo richiede. I BLOB possono essere distribuiti in più server in ordine tooscale out toothem di accesso, ma un singolo blob può essere utilizzato solo da un singolo server. Sebbene i BLOB possano essere raggruppati logicamente in contenitori di BLOB, non vi sono implicazioni sul partizionamento derivanti da questo raggruppamento.
* **File**: chiave di partizione hello per un file è account nome + file di nome di condivisione. Ciò significa che tutti i file di una condivisione file sono presenti anche in una singola partizione.
* **Messaggi**: chiave di partizione hello per un messaggio è il nome di account hello + nome di coda, pertanto tutti i messaggi in una coda vengono raggruppati in un'unica partizione ed eseguiti da un singolo server. Code diverse possono essere elaborate da server diversi toobalance hello caricare per tuttavia molti code potrebbe essere un account di archiviazione.
* **Entità**: chiave di partizione hello per un'entità è il nome di account + nome di tabella + chiave di partizione in cui la chiave di partizione hello è il valore di hello di hello necessarie-definito dall'utente **PartitionKey** proprietà per l'entità hello. Tutte le entità con hello stesso valore di chiave di partizione vengono raggruppate in hello stessa partizione ed eseguita da hello stessa partizione server. Si tratta di un toounderstand punto importante nella progettazione dell'applicazione. L'applicazione deve bilanciare i vantaggi di scalabilità hello di distribuzione delle entità in più partizioni con hello correlati all'accesso ai dati di raggruppamento di entità in una singola partizione.  

Toogrouping un vantaggio chiave un set di entità in una tabella in una singola partizione è che le operazioni batch atomiche tooperform possibili tra le entità nella stessa partizione, in quanto non esiste una partizione in un unico server hello. Pertanto, se si desiderano tooperform operazioni batch su un gruppo di entità, si consiglia di raggrupparli con hello stessa chiave di partizione. 

In hello invece, le entità che sono nella stessa tabella, ma dispongono di chiavi di partizione diverso di hello possono essere con carico bilanciato in server differenti, rendendo possibili toohave maggiore scalabilità.

Suggerimenti dettagliati per la progettazione della strategia di partizionamento per le tabelle sono disponibili [qui](https://msdn.microsoft.com/library/azure/hh508997.aspx).

## <a name="see-also"></a>Vedere anche
* [Dettagli prezzi di archiviazione](https://azure.microsoft.com/pricing/details/storage/)
* [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md)
* [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](storage-premium-storage.md)
* [Replica di Archiviazione di Azure](storage-redundancy.md)
* [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](storage-performance-checklist.md)
* [Archiviazione di Microsoft Azure: un servizio di archiviazione cloud a elevata disponibilità con coerenza assoluta](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

