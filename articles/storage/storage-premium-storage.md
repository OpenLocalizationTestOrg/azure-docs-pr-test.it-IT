---
title: Archiviazione Premium aaaHigh prestazioni e Azure dischi gestiti per le macchine virtuali | Documenti Microsoft
description: Informazioni su Archiviazione Premium a prestazioni elevate e dischi gestiti per le VM di Azure. Le VM di Azure serie DS, DSv2 e GS e Fs supportano Archiviazione Premium.
services: storage
documentationcenter: 
author: ramankumarlive
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: ramankum
ms.openlocfilehash: 2474fa75116fe394672fde48520441fa80cf434f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-premium-storage-and-managed-disks-for-vms"></a>Archiviazione Premium a prestazioni elevate e dischi gestiti per le VM
Archiviazione Premium di Azure offre prestazioni elevate e supporto per dischi a bassa latenza per le macchine virtuali (VM) con carichi di lavoro con I/O intensivo. I dischi delle VM che usano Archiviazione Premium memorizzano i dati in unità a stato solido (SSD). tootake vantaggio della velocità di hello e le prestazioni dei dischi di archiviazione premium, è possibile eseguire la migrazione tooPremium dischi di macchina virtuale esistente archiviazione.

In Azure, è possibile collegare più tooa dischi di archiviazione premium macchina virtuale. L'utilizzo di più dischi offre le applicazioni di too256 TB di spazio di archiviazione per ogni macchina virtuale. Con l'archiviazione Premium, è possono ottenere le applicazioni 80.000 operazioni dei / o al secondo (IOPS) per ogni macchina virtuale e una velocità effettiva del disco di backup too2, 000 megabyte al secondo (MB/s) per ogni macchina virtuale. Le operazioni di lettura offrono una latenza molto bassa.

Con l'archiviazione Premium, Azure offre il possibilità hello tootruly accuratezza di spostamento e applicazioni aziendali complesse come Dynamics AX, Dynamics CRM, Exchange Server, SAP Business Suite e SharePoint cloud toohello farm. È possibile eseguire carichi di lavoro del database a prestazioni intensive in applicazioni come SQL Server, Oracle, MongoDB, MySQL e Redis, che richiedono prestazioni elevate e coerenti e una bassa latenza.

> [!NOTE]
> Per prestazioni ottimali di hello per l'applicazione, è consigliabile eseguire la migrazione i dischi di macchina virtuale che richiede tooPremium IOPS elevata archiviazione. Se il disco non richiede un numero elevato di IOPS, è possibile limitare i costi mantenendolo nel servizio di archiviazione Standard. L'archiviazione Standard archivia i dati dei dischi delle VM in unità disco rigido anziché in unità SSD.
> 

Azure offre due modi i dischi di archiviazione premium toocreate per le macchine virtuali:

* **Dischi non gestiti**

    metodo originale Hello è dischi toouse non gestita. In un disco non gestito, gestire account di archiviazione hello utilizzare file di disco rigido virtuale (VHD) di hello toostore corrispondenti tooyour dischi di macchina virtuale. I file VHD vengono archiviati come BLOB di pagine in account di archiviazione di Azure. 

* **Dischi gestiti**

    Quando si sceglie [dischi gestiti di Azure](storage-managed-disks-overview.md), Azure gestisce gli account di archiviazione hello utilizzati per i dischi di macchina virtuale. Specificare tipo di disco hello (Standard o Premium) e dimensioni di hello del disco hello che è necessario. Azure crea e gestisce disco hello per l'utente. Non è necessario tooworry sull'inserimento di dischi hello in più tooensure gli account di archiviazione che rientrino nei limiti di scalabilità per gli account di archiviazione. Azure gestisce tutto questo automaticamente.

Si consiglia di scegliere i dischi gestiti tootake sfruttare le numerose funzionalità.

tooget avviato con l'archiviazione Premium, [creare l'account di Azure gratuita](https://azure.microsoft.com/pricing/free-trial/). 

Per informazioni sulla migrazione il tooPremium macchine virtuali esistenti di archiviazione, vedere [convertire una macchina virtuale Windows da dischi di dischi non gestito toomanaged](../virtual-machines/virtual-machines-windows-convert-unmanaged-to-managed-disks.md) o [convertire una VM Linux da dischi di dischi non gestito toomanaged](../virtual-machines/linux/convert-unmanaged-to-managed-disks.md).

> [!NOTE]
> Archiviazione Premium è disponibile in molte aree geografiche. Per elenco hello delle aree disponibili, in [servizi di Azure dall'area](https://azure.microsoft.com/regions/#services), esaminare le aree in cui hello supportate macchine virtuali di dimensioni serie di supporto Premium (DS-series, DSV2-series, GS-series e le macchine virtuali serie Fs) sono supportati.
> 

## <a name="features"></a>Funzionalità

Ecco alcune delle funzionalità di hello di archiviazione Premium:

* **Limiti dei dischi di Archiviazione Premium**

    I dischi Premium archiviazione supporta VM che possono essere collegati serie toospecific dimensioni macchine virtuali. L'archiviazione Premium supporta le macchine virtuali serie DS, DSv2, GS, Ls e Fs. È possibile scegliere fra sette dimensioni di disco: P4 (32 GB), P6 (64 GB), P10 (128 GB), P20 (512 GB), P30 (1024 GB), P40 (2048 GB), P50 (4095 GB). Attualmente le dimensioni di disco P4 e P6 sono supportate solo per Managed Disks. Ciascuna dimensione di disco ha le proprie specifiche in termini di prestazioni. A seconda dei requisiti dell'applicazione, è possibile collegare uno o più dischi tooyour macchina virtuale. Vengono descritte le specifiche di hello in modo più dettagliato in [obiettivi di scalabilità e prestazioni di archiviazione Premium](#scalability-and-performance-targets).

* **BLOB di pagine Premium**

    Archiviazione Premium supporta i BLOB di pagine. BLOB di pagine di utilizzare dischi di toostore persistente e non gestito per le macchine virtuali in archiviazione Premium. A differenza di Archiviazione Standard, Archiviazione Premium non supporta i BLOB in blocchi, i BLOB di aggiunta, file, tabelle o code. BLOB di pagine Premium supporta sei dimensioni che vanno da P10 tooP50 e P60 (8191GiB). Blob di pagine P60 Premium non è supportato toobe collegati come dischi di macchina virtuale. 

    Qualsiasi oggetto inserito in un account di Archiviazione Premium è un BLOB di pagine. Consente di agganciare i blob di pagine Hello tooone di hello supportato dimensioni provisioning. È per questo motivo un account di archiviazione premium non è toobe utilizzato toostore BLOB di piccole dimensioni.

* **Account di archiviazione Premium**

    toostart con archiviazione Premium, creare un account di archiviazione premium per i dischi non gestiti. In hello [portale di Azure](https://portal.azure.com), toocreate un account di archiviazione premium, scegliere hello **Premium** livello di prestazioni. Seleziona hello **archiviazione localmente ridondante (LRS)** l'opzione di replica. È inoltre possibile creare un account di archiviazione premium, impostando tipo hello troppo**Premium_LRS** in uno dei hello posizioni seguenti:
    * [API REST di archiviazione](https://docs.microsoft.com/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference) (versione 2014-02-14 o versione successiva)
    * [API REST di gestione servizi](http://msdn.microsoft.com/library/azure/ee460799.aspx) (versione 2014-10-01 o una versione successiva; per le distribuzioni di Azure classiche)
    * [API REST del provider delle risorse di archiviazione di Azure](https://docs.microsoft.com/rest/api/storagerp) (per le distribuzioni di Azure Resource Manager)
    * [Azure PowerShell](../powershell-install-configure.md) (versione 0.8.10 o successiva)

    toolearn sui limiti dell'account di archiviazione premium, vedere [obiettivi di scalabilità e prestazioni di archiviazione Premium](#premium-storage-scalability-and-performance-targets).

* **Archiviazione Premium con ridondanza locale**

    Un account di archiviazione premium supporta solo archiviazione con ridondanza locale come opzione di replica hello. Archiviazione con ridondanza locale mantiene tre copie dei dati hello all'interno di una singola area. Per eseguire il ripristino di emergenza dell'area, è necessario eseguire il backup dei dischi delle VM in un'altra area usando il [Backup di Azure](../backup/backup-introduction-to-azure-backup.md). È inoltre necessario utilizzare un account di archiviazione con ridondanza geografica (GRS) come archivio di backup hello. 

    Azure usa l'account di archiviazione come contenitore per i dischi non gestiti. Quando si crea una VM di Azure serie DS, DSv2, GS o Fs con dischi non gestiti e si seleziona un account di archiviazione Premium, il sistema operativo e i dischi dati vengono archiviati in tale account.

## <a name="supported-vms"></a>VM supportate
L'archiviazione Premium supporta le macchine virtuali serie DS, DSv2, GS, Ls e Fs. Con questi tipi di VM è possibile usare dischi di archiviazione sia Standard che Premium. Non è possibile usare i dischi di Archiviazione Premium con MV delle serie non compatibili con Archiviazione Premium.

Per informazioni sui tipi e le dimensioni delle VM in Azure, vedere [Dimensioni delle macchine virtuali Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Per informazioni sui tipi e le dimensioni delle VM in Azure, vedere [Dimensioni delle macchine virtuali Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Queste sono alcune delle funzionalità di hello di hello DS-series, DSv2-series, GS-series, Ls serie e le macchine virtuali serie Fs:

* **Servizio cloud**

    È possibile aggiungere del servizio cloud di macchine virtuali serie DS tooa contenente solo le macchine virtuali serie DS. Non aggiungere le macchine virtuali serie DS tooan servizio cloud esistente dotato di tipo diverso da macchine virtuali serie DS. È possibile migrare i dischi rigidi virtuali tooa nuovo servizio cloud esistente che esegue solo le macchine virtuali serie DS. Se si desidera toouse hello dello stesso indirizzo IP virtuale per hello nuovo servizio cloud che ospita le macchine virtuali serie DS, utilizzare [indirizzi IP riservati](../virtual-network/virtual-networks-instance-level-public-ip.md). È possibile aggiungere le macchine virtuali GS-series servizio cloud esistente tooan contenente solo le macchine virtuali GS-series.

* **Disco del sistema operativo**

    È possibile impostare la macchina virtuale di archiviazione Premium di toouse premium o un disco del sistema operativo standard. Per un'esperienza ottimale hello, è consigliabile utilizzare un disco del sistema operativo basato su archiviazione Premium.

* **Dischi dati**

    È possibile utilizzare premium e standard dischi hello stessa macchina virtuale di archiviazione Premium. Con l'archiviazione Premium, è possibile eseguire il provisioning di una macchina virtuale e collegare diversi dati persistenti dischi toohello macchina virtuale. Se necessario, tooincrease hello capacità e prestazioni del volume di hello, è possibile eseguire lo striping tra i dischi.

    > [!NOTE]
    > Se si esegue lo striping dei dischi dati di Archiviazione Premium mediante [Spazi di archiviazione](http://technet.microsoft.com/library/hh831739.aspx), è consigliabile configurare gli spazi di archiviazione con 1 colonna per ogni disco utilizzato. In caso contrario, complessivo delle prestazioni del volume con striping hello potrebbero essere inferiore al previsto a causa di una distribuzione non uniforme del traffico tra dischi hello. Per impostazione predefinita, in Server Manager, è possibile impostare le colonne per i dischi too8. Se si dispone di più di 8 dischi, utilizzare volume hello toocreate di PowerShell. Specificare il numero di hello colonne manualmente. In caso contrario, Server Manager UI hello continua toouse 8 colonne, anche se si dispone di più dischi. Ad esempio, se si desidera gestire 32 dischi in un unico striping, è necessario specificare 32 colonne. numero di hello toospecify colonne hello Usa disco virtuale, in hello [New-VirtualDisk](http://technet.microsoft.com/library/hh848643.aspx) cmdlet di PowerShell, usare hello *NumberOfColumns* parametro. Per altre informazioni, vedere [Panoramica sugli spazi di archiviazione](http://technet.microsoft.com/library/hh831739.aspx) e [Domande frequenti sugli spazi di archiviazione](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx).
    >
    > 

* **Cache**

    Macchine virtuali in una serie di dimensioni hello che supportano l'archiviazione Premium sono una funzionalità di memorizzazione nella cache univoca per i livelli elevati di velocità effettiva e latenza. funzionalità di memorizzazione nella cache di Hello supera le prestazioni del disco di archiviazione premium sottostante. È possibile impostare il disco di hello criterio nei dischi di archiviazione premium di cache troppo**ReadOnly**, **ReadWrite**, o **Nessuno**. criteri di memorizzazione nella cache di Hello predefinito disco **ReadOnly** per tutti i dischi premium, dati e **ReadWrite** per i dischi del sistema operativo. Per ottenere prestazioni ottimali per l'applicazione, utilizzare hello correggere l'impostazione della cache. Ad esempio, per i dischi di dati elevati in termini di lettura o di sola lettura, ad esempio i file di dati di SQL Server, impostare il disco di hello la memorizzazione nella cache dei criteri troppo**ReadOnly**. Per i dischi di dati elevati in termini di scrittura o sola scrittura, ad esempio i file di log di SQL Server, impostare disco hello la memorizzazione nella cache dei criteri troppo**Nessuno**. toolearn più sull'ottimizzazione di progettazione con l'archiviazione Premium, vedere [struttura per le prestazioni con archiviazione Premium](storage-premium-storage-performance.md).

* **Analisi**

    prestazioni della macchina virtuale tooanalyze utilizzando i dischi di archiviazione Premium, attivare la diagnostica VM in hello [portale di Azure](https://portal.azure.com). Per altre informazioni, vedere [Azure VM monitoring with Azure Diagnostics Extension](https://azure.microsoft.com/blog/2014/09/02/windows-azure-virtual-machine-monitoring-with-wad-extension/) (Monitoraggio delle VM di Azure con Estensione di Diagnostica di Azure). 

    le prestazioni del disco toosee, utilizzare strumenti basati sul sistema operativo come [Windows Performance Monitor](https://technet.microsoft.com/library/cc749249.aspx) per macchine virtuali di Windows e hello [iostat](http://linux.die.net/man/1/iostat) comando per le macchine virtuali Linux.

* **Limiti di scalabilità e prestazioni delle VM**

    Ogni dimensione di macchina virtuale supportate archiviazione Premium i limiti di scalabilità e specifiche delle prestazioni per IOPS, della larghezza di banda e numero di hello di dischi che possono essere associati per ogni macchina virtuale. Quando si usano i dischi di archiviazione premium con macchine virtuali, assicurarsi che sia sufficiente e larghezza di banda del traffico di disco toodrive macchina virtuale.

    Ad esempio, una VM STANDARD_DS1 ha un larghezza di banda dedicata di 32 MB/s per il traffico nei dischi di archiviazione Premium. Un disco di Archiviazione Premium P10 può offrire una larghezza di banda di 100 MB/s. Se un disco di archiviazione premium P10 toothis collegato VM, è possibile tornare solo backup too32 MB/s. Non può utilizzare hello che massimo 100 MB/s disco P10 hello può fornire.

    Attualmente, hello VM più grande in hello serie DS è hello Standard_DS15_v2. Hello Standard_DS15_v2 può fornire backup too960 MB/s in tutti i dischi. Hello VM più grande in GS-series hello è hello Standard_GS5. Hello Standard_GS5 può fornire backup too2, 000 MB/s in tutti i dischi.

    Si noti che questi limiti riguardano solo il traffico su disco. Questi limiti non includono i riscontri cache e il traffico di rete. Una larghezza di banda separata è disponibile per il traffico di rete della VM. Larghezza di banda per il traffico di rete è diverso da hello dedicato larghezza di banda per i dischi di archiviazione premium.

    Per hello informazioni più aggiornate sui massimo di IOPS e la velocità effettiva (larghezza di banda) per macchine virtuali con archiviazione Premium-supportati, vedere [dimensioni delle macchine Virtuali di Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [le dimensioni di VM Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

    Per ulteriori informazioni sui dischi di archiviazione premium e i relativi limiti di velocità effettiva e IOPS, vedere la tabella hello nella sezione successiva hello.

## <a name="scalability-and-performance-targets"></a>Obiettivi di scalabilità e prestazioni
In questa sezione si descrivono tooconsider di destinazioni di scalabilità e prestazioni hello quando si utilizza l'archiviazione Premium.

Account di archiviazione Premium sono hello le destinazioni di scalabilità seguenti:

| Capacità account totale | Larghezza di banda totale per un account di archiviazione con ridondanza locale |
| --- | --- | 
| Capacità disco: 35 TB <br>Capacità snapshot: 10 TB | Backup too50 Gigabit al secondo per connessioni in entrata<sup>1</sup> + in uscita<sup>2</sup> |

<sup>1</sup> tutti i dati (richieste) inviati tooa account di archiviazione

<sup>2</sup> Tutti i dati (risposte) ricevuti da un account di archiviazione

Per altre informazioni, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md).

Se si utilizza l'account di archiviazione premium per i dischi non gestiti e l'applicazione si superano le destinazioni di scalabilità hello di un singolo account di archiviazione, è possibile toomigrate toomanaged dischi. Se non si desidera toomigrate toomanaged dischi, compilare l'applicazione toouse più account di archiviazione. Quindi partizionare i dati tra tali account di archiviazione. Ad esempio, se si desidera dischi 51 TB tooattach tra più macchine virtuali, distribuirli in due account di archiviazione. 35 TB è il limite di hello per un account di archiviazione premium singolo. Accertarsi che i dischi di cui viene effettuato il provisioning in un singolo account di archiviazione Premium non superino mai i 35 TB.

### <a name="premium-storage-disk-limits"></a>Limiti dei dischi di Archiviazione Premium
Quando si provisioning di un disco di archiviazione premium, dimensioni hello del disco hello determina hello massimo IOPS e la velocità effettiva (larghezza di banda). Azure offre sette tipi di dischi di Archiviazione Premium: P4 (solo Managed Disks), P6 (solo Managed Disks), P10, P20, P30, P40 e P50. Ogni tipo di disco di Archiviazione Premium ha limiti specifici di IOPS e velocità effettiva. In hello nella tabella seguente vengono descritti i limiti per i tipi di disco hello:

| Tipo di disco Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Dimensioni disco           | 32 GB| 64 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPS per disco       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Velocità effettiva per disco | 25 MB al secondo  | 50 MB al secondo  | 100 MB al secondo | 150 MB al secondo | 200 MB al secondo | 250 MB al secondo | 250 MB al secondo | 

> [!NOTE]
> Assicurarsi che la larghezza di banda sufficiente sia disponibile sul traffico di disco toodrive macchina virtuale, come descritto in [macchine virtuali con archiviazione Premium-supportata](#premium-storage-supported-vms). In caso contrario, la velocità effettiva del disco e IOPS è vincolata toolower valori. Velocità effettiva massima e IOPS sono basati sui limiti della macchina virtuale hello, non sui limiti di disco hello descritti nella tabella precedente hello.  
> 
> 

Ecco alcuni aspetti importanti di tooknow sulle destinazioni di scalabilità e prestazioni di archiviazione Premium:

* **Capacità fornita e prestazioni**

    Quando si esegue il provisioning di un disco di archiviazione premium, a differenza di archiviazione standard, si ha la garanzia capacità hello, IOPS e la velocità effettiva del disco. Se ad esempio si crea un disco P50, Azure effettua il provisioning di 4.095 GB di capacità di archiviazione, 7.500 IOPS e 250 MB/s di velocità effettiva per tale disco. L'applicazione può utilizzare tutta o parte di hello capacità e prestazioni.

* **Dimensioni disco**

    Mappe Azure hello toohello (arrotondata per eccesso) di dimensioni di disco più vicino opzione disco di archiviazione premium, come specificato nella tabella hello nella precedente sezione hello. Ad esempio, una dimensione del disco di 100 GB viene classificata come opzione P10. È possibile eseguire backup too500 IOPS, con backup di velocità effettiva di too100 MB/s. Analogamente, un disco di 400 GB viene classificato come P20. È possibile eseguire backup too2, 300 IOPS, con velocità effettiva di 150 MB/s.
    
    > [!NOTE]
    > È possibile aumentare facilmente dimensioni hello di dischi esistenti. Ad esempio, desiderato dimensioni hello tooincrease di 30 GB disco too128 GB o TB too1 anche. In alternativa, è consigliabile tooconvert il disco di tooa P30 P20 perché è necessario maggiore capacità o altre operazioni IOPS e la velocità effettiva. 
    > 
 
* **Dimensioni di I/O**

    Hello di un / o è 256 KB. Se i dati di hello trasferiti sono inferiore a 256 KB, viene considerato 1 unità dei / o. Le dimensioni di I/O superiori vengono calcolate come più I/O da 256 KB. Ad esempio, 1.100 KB di I/O corrispondono a 5 unità di I/O.

* **Velocità effettiva**

    il limite di velocità effettiva di Hello include scritture toohello disco e include le operazioni di lettura disco che non sono soddisfatte dalla cache di hello. Ad esempio, un disco P10 ha una velocità effettiva di 100 MB/s per disco. In hello nella tabella seguente sono illustrati alcuni esempi di velocità effettiva valida per un disco P10:

    | Velocità effettiva massima per un disco P10 | Letture non cache dal disco | Operazioni di scrittura della cache non toodisk |
    | --- | --- | --- |
    | 100 MB/s | 100 MB/s | 0 |
    | 100 MB/s | 0 | 100 MB/s |
    | 100 MB/s | 60 MB/s | 40 MB/s |

* **Riscontri cache**

    Riscontri nella cache non sono limitate dalle hello allocata IOPS o una velocità effettiva del disco hello. Ad esempio, quando si utilizza un disco dati con un **ReadOnly** impostazione della cache in una macchina virtuale supportate da archiviazione Premium, le letture che vengono soddisfatte dalla cache di hello non è soggetto toohello IOPS e delimitatori di velocità effettiva del disco hello. Se il carico di lavoro hello di un disco è prevalentemente legge, è possibile ottenere una velocità effettiva molto elevata. cache di Hello è soggetto tooseparate IOPS e i limiti di velocità effettiva in hello livello macchina virtuale, in base alle dimensioni della macchina virtuale hello. Le VM della serie DS hanno circa 4.000 IOPS e 33 MB/s per memoria centrale per la cache e gli I/O dell'unità SSD locale. Le VM della serie GS hanno circa 5.000 IOPS e 50 MB/s per memoria centrale per la cache e gli I/O dell’unità SSD locale. 

## <a name="throttling"></a>Limitazione
La limitazione delle richieste potrebbe verificarsi se l'applicazione IOPS o una velocità effettiva supera i limiti di hello allocato per un disco di archiviazione premium. La limitazione delle richieste potrebbe verificarsi anche se il traffico totale su disco in tutti i dischi nella macchina virtuale hello supera il limite della larghezza di banda di disco hello è disponibile per hello macchina virtuale. tooavoid limitazione, è consigliabile limitare hello numero di richieste dei / o disco hello in sospeso. Usare un limite in base alle destinazioni di scalabilità e prestazioni per il disco di hello che è stato effettuato il provisioning e hello disco della larghezza di banda disponibile toohello macchina virtuale.  

L'applicazione può ottenere la latenza più bassa di hello quando si è progettato tooavoid la limitazione delle richieste. Tuttavia, se hello numero di richieste in sospeso i/o per il disco di hello è troppo piccolo, l'applicazione non è possibile usufruire di hello livelli massimi di IOPS e la velocità effettiva che sono disponibili toohello disco.

Hello seguenti esempi illustrano come la limitazione delle richieste di toocalculate livelli. Tutti i calcoli sono basati su una dimensione dell'unità di I/O pari a 256 KB.

### <a name="example-1"></a>Esempio 1
L'applicazione ha elaborato 495 unità di I/O da 16 KB in un disco P10. unità dei / o Hello vengono conteggiate come 495 IOPS. Se si tenta un / o di 2 MB in hello stesso secondo, totale hello di unità dei / o è uguale too495 + 8 IOPS. Infatti, i/o di 2 MB = unità 2.048 KB / 256 KB = 8 i/o, in caso di hello dimensioni dell'unità dei / o è di 256 KB. Poiché la somma hello 495 + 8 supera limite di IOPS per disco hello 500 hello, si verifica una limitazione.

### <a name="example-2"></a>Esempio 2
L'applicazione ha elaborato 400 unità di I/O da 256 KB in un disco P10. Hello larghezza di banda totale utilizzata (400 &#215; 256) / 1.024 KB = 100 MB/s. Il limite di velocità effettiva di un disco P10 è 100 MB al secondo. Se l'applicazione tenta tooperform ulteriori operazioni dei / o il secondo, si è limitato perché supera il limite di hello allocata.

### <a name="example-3"></a>Esempio 3
Si dispone di una macchina virtuale DS4 con due dischi P30 collegati. Ogni disco P30 è in grado di supportare una velocità effettiva pari a 200 MB/s. Tuttavia, una VM DS4 ha una capacità di larghezza di banda su disco totale pari a 256 MB/s. Non è possibile guidare entrambi i dischi collegati toohello la velocità effettiva massima su questa macchina virtuale DS4 in hello contemporaneamente. tooresolve, è in grado di sostenere il traffico di 200 MB/s in un disco e 56 MB/s in hello altro disco. Se la somma hello del traffico disco passa nel 256 MB/s, il traffico su disco è limitato.

> [!NOTE]
> Se il traffico del disco è costituita principalmente da di piccole dimensioni dei / o, l'applicazione probabilmente verrà raggiunto il limite di IOPS hello prima il limite di velocità effettiva di hello. Tuttavia, se traffico disco hello è costituita principalmente da di grandi dimensioni dei / o, l'applicazione probabilmente verrà raggiunto il limite di velocità effettiva di hello in primo luogo, anziché il limite di IOPS hello. È possibile ottimizzare il numero di IOPS dell'applicazione e la capacità di velocità effettiva con dimensioni ottimali dell'I/O. Inoltre, è possibile limitare il numero hello di richieste in sospeso i/o per un disco.
> 

toolearn ulteriori informazioni sulla progettazione per prestazioni elevate con archiviazione Premium, vedere [struttura per le prestazioni con archiviazione Premium](storage-premium-storage-performance.md).

## <a name="snapshots-and-copy-blob"></a>Snapshot e Copia BLOB

il servizio di archiviazione, file VHD hello toohello è un blob di pagine. È possibile creare snapshot del BLOB di pagine e copiarli tooanother percorso, ad esempio account di archiviazione diverso tooa.

### <a name="unmanaged-disks"></a>Dischi non gestiti

Creare [snapshot incrementali](storage-incremental-snapshots.md) per i dischi premium non gestito hello stessa modalità di utilizzo di snapshot con archiviazione standard. Archiviazione Premium supporta solo archiviazione con ridondanza locale come opzione di replica hello. È consigliabile creare snapshot e quindi copiare account di archiviazione standard con ridondanza geografica tooa snapshot hello. Per altre informazioni, vedere [Opzioni di ridondanza di Archiviazione di Azure](storage-redundancy.md).

Se un disco collegato tooa VM, è possibile che alcune operazioni API su disco hello non sono consentite. Ad esempio, non è possibile eseguire un [Copy Blob](/rest/api/storageservices/Copy-Blob) operazione per tale blob se hello disco è collegato tooa macchina virtuale. In alternativa, è possibile creare innanzitutto uno snapshot del blob utilizzando hello [Snapshot Blob](/rest/api/storageservices/Snapshot-Blob) API REST. Eseguire quindi hello [Copy Blob](/rest/api/storageservices/Copy-Blob) di hello toocopy di hello snapshot disco collegato. In alternativa, è possibile scollegare il disco hello e quindi effettuare le operazioni necessarie.

Hello seguendo i limiti si applica gli snapshot di blob di archiviazione toopremium:

| Limite di Archiviazione Premium | Valore |
| --- | --- |
| Massimo numero di snapshot per BLOB | 100 |
| Capacità dell'account di archiviazione per gli snapshot<br>(Include i dati solo degli snapshot; non include i dati del BLOB di base.) | 10 TB |
| Minimo tempo tra snapshot consecutivi | 10 minuti |

toomaintain copie con ridondanza geografica degli snapshot, è possibile copiare gli snapshot da un account di archiviazione standard con ridondanza geografica premium storage account tooa tramite AzCopy o Blob di copia. Per ulteriori informazioni, vedere [trasferire i dati con l'utilità della riga di comando di hello AzCopy](storage-use-azcopy.md) e [Copy Blob](/rest/api/storageservices/Copy-Blob).

Per informazioni dettagliate sull'esecuzione di operazioni REST sui BLOB di pagine negli account di archiviazione Premium, vedere [Using Blob Service Operations with Azure Premium Storage](http://go.microsoft.com/fwlink/?LinkId=521969) (Uso delle operazioni del servizio BLOB con Archiviazione Premium di Azure).

### <a name="managed-disks"></a>Dischi gestiti

Uno snapshot per un disco gestito è una copia di sola lettura del disco gestito hello. Hello snapshot viene archiviato come un disco gestito standard. Attualmente gli [snapshot incrementali](storage-incremental-snapshots.md) non sono supportati per i dischi gestiti. toolearn tootake uno snapshot per un disco gestito, vedere [creare una copia di un disco rigido virtuale archiviato come un Azure gestita disco utilizzando Windows gestito snapshot](../virtual-machines/virtual-machines-windows-snapshot-copy-managed-disk.md) o [creare una copia di un disco rigido virtuale archiviato come un Azure gestita disco utilizzando gestiti gli snapshot in Linux](../virtual-machines/linux/snapshot-copy-managed-disk.md).

Se un disco gestito è collegato tooa VM, è possibile che alcune operazioni API su disco hello non sono consentite. È ad esempio, non è possibile generare un tooperform di firma di accesso condiviso un'operazione di copia mentre il disco di hello è collegato tooa macchina virtuale. In alternativa, creare innanzitutto uno snapshot del disco hello e quindi eseguire Copia hello dello snapshot hello. In alternativa, è possibile scollegare il disco hello e quindi generare un'operazione di copia hello tooperform SAS.


## <a name="premium-storage-for-linux-vms"></a>Archiviazione Premium per VM Linux
È possibile utilizzare hello seguente toohelp informazioni che configurare le macchine virtuali Linux in archiviazione Premium:

scalabilità tooachieve destinato nell'archiviazione Premium, per tutti i dischi di archiviazione premium con di memorizzare nella cache set troppo**ReadOnly** o **Nessuno**, è necessario disabilitare "barriere" quando si monta sistema file hello. Barriere in questo scenario non è necessario perché hello scrive toopremium dischi di archiviazione sono durevoli per tali impostazioni della cache. Quando viene completata correttamente la richiesta di scrittura hello, sono stati scritti dati toohello un archivio permanente. toodisable "barriere", utilizzare uno dei seguenti metodi hello. Scegliere hello per il file system:
  
* Per **reiserFS**, toodisable barriere, utilizzare hello `barrier=none` montare opzione. (utilizzare barriere tooenable, `barrier=flush`.)
* Per **ext3/ext4**, toodisable barriere, utilizzare hello `barrier=0` montare opzione. (utilizzare barriere tooenable, `barrier=1`.)
* Per **XFS**, toodisable barriere, utilizzare hello `nobarrier` montare opzione. (utilizzare barriere tooenable, `barrier`.)
* Per i dischi di archiviazione premium con cache troppo impostare**ReadWrite**, abilitare barriere per la durabilità di scrittura.
* Per toopersist etichette di volume dopo il riavvio hello macchina virtuale, è necessario aggiornare /etc/fstab. con hello identificatore univoco universale (UUID) riferimenti toohello dischi. Per ulteriori informazioni, vedere [aggiungere tooa un disco gestito VM Linux](../virtual-machines/linux/add-disk.md).

Hello seguendo le distribuzioni di Linux è stato convalidato per l'archiviazione di Azure Premium. Per migliorare le prestazioni e stabilità con archiviazione Premium, è consigliabile effettuare l'aggiornamento tooone le macchine virtuali di queste versioni, come minimo (tooa o versione successiva). Alcune versioni richiedono hello hello più recente Linux Integration Services (LIS), v 4.0, per Azure. toodownload e installare una distribuzione, seguire il collegamento di hello elencato nella tabella seguente hello. Elenco di immagini toohello aggiungiamo durante il completamento della convalida. Si noti che le nostre convalide mostrano che le prestazioni variano per ogni immagine. Le prestazioni dipendono dalle caratteristiche del carico di lavoro e dalle impostazioni. Immagini diverse sono ottimizzate per tipi di carico di lavoro diversi.

| Distribuzione | Versione | Kernel supportato | Dettagli |
| --- | --- | --- | --- |
| Ubuntu | 12.04 | 3.2.0-75.110+ | Ubuntu-12_04_5-LTS-amd64-server-20150119-en-us-30GB |
| Ubuntu | 14.04 | 3.13.0-44.73+ | Ubuntu-14_04_1-LTS-amd64-server-20150123-en-us-30GB |
| Debian | 7.x, 8.x | 3.16.7-ckt4-1+ | &nbsp; |
| SUSE | SLES 12| 3.12.36-38.1+| suse-sles-12-priority-v20150213 <br> suse-sles-12-v20150213 |
| SUSE | SLES 11 SP4 | 3.0.101-0.63.1+ | &nbsp; |
| CoreOS | 584.0.0+| 3.18.4+ | CoreOS 584.0.0 |
| CentOS | 6.5, 6.6, 6.7, 7.0 | &nbsp; | [LIS4 richiesto](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Vedere la nota nella sezione successiva hello* |
| CentOS | 7.1+ | 3.10.0-229.1.2.el7+ | [LIS4 consigliato](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Vedere la nota nella sezione successiva hello* |
| Red Hat Enterprise Linux (RHEL) | 6.8+, 7.2+ | &nbsp; | &nbsp; |
| Oracle | 6.0+, 7.2+ | &nbsp; | UEK4 o RHCK |
| Oracle | 7.0-7.1 | &nbsp; | UEK4 or RHCK con [LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |
| Oracle | 6.4-6.7 | &nbsp; | UEK4 or RHCK con [LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |


### <a name="lis-drivers-for-openlogic-centos"></a>Driver LIS per Openlogic CentOS

Se si eseguono le macchine virtuali di OpenLogic CentOS, eseguire hello driver più recenti hello tooinstall di comando seguente:

```
sudo rpm -e hypervkvpd  ## (Might return an error if not installed. That's OK.)
sudo yum install microsoft-hyper-v
```

tooactivate hello nuovi driver, riavviare il computer di hello.

## <a name="pricing-and-billing"></a>Prezzi e fatturazione

Quando si utilizza l'archiviazione Premium, si applica hello fatturazione considerazioni seguenti:

* **Dimensione del BLOB e del disco di Archiviazione Premium**

    La fatturazione per un blob o il disco di archiviazione premium dipende dalle dimensioni hello il provisioning del disco hello o blob. Mappe Azure hello toohello dimensioni provisioning (arrotondata per eccesso) più vicino opzione disco di archiviazione premium. Per informazioni dettagliate, vedere la tabella hello in [obiettivi di scalabilità e prestazioni di archiviazione Premium](#premium-storage-scalability-and-performance-targets). Ogni tooa mappe disco supportato il provisioning delle dimensioni del disco e viene fatturato di conseguenza. La fatturazione per i dischi di provisioning viene ripartita oraria con prezzo mensile hello offerta di archiviazione Premium hello. Ad esempio, se è stato eseguito il provisioning di un disco P10 ed eliminata dopo 20 ore, vengono fatturati per hello P10 offerta ripartito too20 ore. Si tratta indipendentemente dalla quantità di hello di dati effettivi scritti su disco toohello o hello IOPS e la velocità effettiva utilizzata.

* **Snapshot dei dischi non gestiti Premium**

    Snapshot su dischi premium non gestiti non vengono fatturate per una capacità aggiuntiva hello utilizzata dagli snapshot hello. Per altre informazioni sugli snapshot, vedere [Creazione di uno snapshot di un BLOB](/rest/api/storageservices/Snapshot-Blob).

* **Snapshot dei dischi gestiti Premium**

    Uno snapshot di un disco gestito è una copia di sola lettura del disco hello. disco Hello viene archiviato come un disco gestito standard. I costi di una snapshot hello stessa come disco di gestita standard. Ad esempio, se si crea uno snapshot di un disco gestito premium 128 GB, il costo di hello dello snapshot hello è disco gestito standard di tooa equivalente 128 GB.  

* **Trasferimenti di dati in uscita**

    I [trasferimenti di dati in uscita](https://azure.microsoft.com/pricing/details/data-transfers/) (dati in uscita dai data center di Azure) vengono fatturati in base all'utilizzo di larghezza di banda.

Per informazioni dettagliate sui prezzi di Archiviazione Premium, sulle VM supportate da Archiviazione Premium e su Managed Disks, vedere questi articoli:

* [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/)
* [Prezzi delle macchine virtuali](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Prezzi di Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks/)

## <a name="azure-backup-support"></a>Supporto di Backup di Azure 

Per eseguire il ripristino di emergenza dell'area, è necessario eseguire il backup dei dischi delle VM in un'altra area usando [Backup di Azure](../backup/backup-introduction-to-azure-backup.md) e un account di archiviazione con ridondanza geografica come insieme di credenziali di backup.

toocreate un processo di backup con backup basate sul tempo, facilmente ripristinati VM e i criteri di conservazione dei backup, utilizzare Backup di Azure. È possibile usare Backup con dischi gestiti e non gestiti. Per altre informazioni, vedere [Backup di macchine virtuali di Azure in insiemi di credenziali di Servizi di ripristino](../backup/backup-azure-vms-first-look-arm.md) e [Uso delle macchine virtuali con dischi gestiti con Backup di Azure](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). 

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sull'archiviazione Premium, vedere hello seguenti articoli.

### <a name="design-and-implement-with-premium-storage"></a>Progettare e implementare con Archiviazione Premium
* [Progettare ai fini delle prestazioni con Archiviazione Premium](storage-premium-storage-performance.md)
* [Operazioni di archiviazione BLOB con Archiviazione Premium](http://go.microsoft.com/fwlink/?LinkId=521969)

### <a name="operational-guidance"></a>Informazioni operative
* [Eseguire la migrazione tooAzure archiviazione Premium](storage-migration-to-premium-storage.md)

### <a name="blog-posts"></a>Post di BLOG
* [Archiviazione Premium di Azure disponibile a livello generale](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/)
* [Annuncio hello GS-series: aggiunta di toohello di supporto di archiviazione Premium più grande di macchine virtuali in hello cloud pubblico](https://azure.microsoft.com/blog/azure-has-the-most-powerful-vms-in-the-public-cloud/)
