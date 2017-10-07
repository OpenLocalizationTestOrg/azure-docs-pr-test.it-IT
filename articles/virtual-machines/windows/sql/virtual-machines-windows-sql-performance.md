---
title: aaaPerformance procedure consigliate per SQL Server in Azure | Documenti Microsoft
description: In questo argomento vengono fornite le procedure consigliate per ottimizzare le prestazioni di SQL Server in Macchine virtuali di Microsoft Azure.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a0c85092-2113-4982-b73a-4e80160bac36
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: jroth
ms.openlocfilehash: 42ec9fbeb2dec3a654b93bbd08d666369835ee73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-best-practices-for-sql-server-in-azure-virtual-machines"></a>Procedure consigliate per le prestazioni per SQL Server in Macchine virtuali di Azure

## <a name="overview"></a>Panoramica

Questo argomento illustra le procedure consigliate per ottimizzare le prestazioni di SQL Server in Macchine virtuali di Microsoft Azure. Durante l'esecuzione di SQL Server in macchine virtuali di Azure, è consigliabile continuare a usare hello stesso database ottimizzazione delle prestazioni opzioni applicabili tooSQL Server nell'ambiente server locale. Tuttavia, prestazioni di hello di un database relazionale in un cloud pubblico dipendono da molti fattori, ad esempio dimensioni hello di una macchina virtuale e la configurazione hello hello di dischi di dati.

Durante la creazione di immagini di SQL Server, [prendere in considerazione il provisioning delle macchine virtuali nel portale di Azure hello](virtual-machines-windows-portal-sql-server-provision.md). Macchine virtuali di SQL Server disponibile nel portale di gestione risorse di hello implementare tutte queste le procedure consigliate, inclusa la configurazione di archiviazione hello.

In questo articolo è incentrato su come ottenere hello *migliore* le prestazioni di SQL Server in macchine virtuali di Azure. Se il carico di lavoro è contenuto, potrebbero non essere necessarie tutte le ottimizzazione elencate di seguito. Prendere in considerazione le esigenze di prestazioni e i modelli di carico di lavoro durante la valutazione di queste indicazioni.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="quick-check-list"></a>Elenco di controllo rapido

di seguito Hello è un elenco di controllo rapido per ottenere prestazioni ottimali di SQL Server in macchine virtuali di Azure:

| Area | Ottimizzazioni |
| --- | --- |
| [Dimensioni macchina virtuale](#vm-size-guidance) |[DS3](../../virtual-machines-windows-sizes-memory.md) o superiore per SQL Enterprise.<br/><br/>[DS2](../../virtual-machines-windows-sizes-memory.md) o superiore per SQL Standard Edition e Web Edition. |
| [Archiviazione](#storage-guidance) |Usare [Archiviazione Premium](../../../storage/common/storage-premium-storage.md). Archiviazione Standard è consigliata solo per i carichi di lavoro di sviluppo/test.<br/><br/>Mantenere hello [account di archiviazione](../../../storage/common/storage-create-storage-account.md) e macchina virtuale di SQL Server in hello stessa area.<br/><br/>Disabilitare Azure [archiviazione con ridondanza geografica](../../../storage/common/storage-redundancy.md) (replica geografica) nell'account di archiviazione hello. |
| [Dischi](#disks-guidance) |Usare almeno 2 [dischi P30](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) (1 per i file di log, 1 per i file di dati e TempDB).<br/><br/>Evitare l'uso del sistema operativo o di dischi temporanei per la registrazione o l'archiviazione di database.<br/><br/>Abilitare la cache di lettura su dischi hello ospita i file di dati hello e TempDB.<br/><br/>Non abilitare la memorizzazione nella cache nei dischi che ospitano i file di log hello.<br/><br/>Importante: Arrestare il servizio di SQL Server hello quando si modificano le impostazioni della cache di hello per un disco di macchina virtuale di Azure.<br/><br/>Eseguire lo striping di velocità effettiva dei / o tooget aumentato di dischi di più dati di Azure.<br/><br/>Formattare con dimensioni di allocazione documentate. |
| [I/O](#io-guidance) |Abilitare la compressione di pagina di database.<br/><br/>Abilitare l'inizializzazione immediata dei file per i file di dati.<br/><br/>Limitare o disabilitare l'aumento automatico delle dimensioni nel database di hello.<br/><br/>Disabilitare la compattazione automatica nel database di hello.<br/><br/>Spostare tutti i dischi toodata database, inclusi i database di sistema.<br/><br/>Spostare l'errore log e trace file directory toodata dischi del Server SQL.<br/><br/>Configurare il percorso predefinito del file di backup e del file di database.<br/><br/>Abilitare le pagine bloccate.<br/><br/>Applicare le correzioni delle prestazioni di SQL Server. |
| [Specifiche della funzione](#feature-specific-guidance) |Eseguire il backup direttamente tooblob archiviazione. |

Per ulteriori informazioni su *come* e *perché* toomake queste ottimizzazioni, controllare i dettagli di hello e informazioni aggiuntive fornite nelle sezioni seguenti.

## <a name="vm-size-guidance"></a>Linee guida per le dimensioni delle VM

Per applicazioni sensibili delle prestazioni, è consigliabile utilizzare la seguente hello [dimensioni delle macchine virtuali](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json):

* **SQL Server Enterprise Edition**: DS3 o superiore
* **SQL Server Standard e Web Edition**: DS2 o superiore

## <a name="storage-guidance"></a>Linee guida per l'archiviazione

Le VM serie DS, oltre alle serie DSv2 e GS, supportano [Archiviazione Premium](../../../storage/common/storage-premium-storage.md). Archiviazione Premium è l'impostazione consigliata per tutti i carichi di lavoro di produzione.

> [!WARNING]
> Archiviazione Standard è caratterizzata da latenze e larghezze di banda variabili ed è consigliata solo per i carichi di lavoro di sviluppo e test. Per i carichi di lavoro di produzione si consiglia di usare Archiviazione Premium.

Inoltre, si consiglia di creare l'account di archiviazione di Azure in hello stesso data center, come i ritardi nel trasferimento tooreduce macchine virtuali SQL Server. Quando si crea un account di archiviazione, disabilitare la replica geografica in quanto l'ordine di scrittura coerente su più dischi non è garantito. In alternativa, si consiglia di configurare una tecnologia di ripristino di emergenza di SQL Server tra due data center di Azure. Per altre informazioni, vedere [Disponibilità elevata e ripristino di emergenza per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="disks-guidance"></a>Linee guida per i dischi

Esistono tre tipi di disco principali in una VM Azure:

* **Disco del sistema operativo**: quando si crea una macchina virtuale di Azure, piattaforma hello assocerà almeno un disco (etichettata come hello **C** unità) toohello macchina virtuale per il disco del sistema operativo. Si tratta di un disco rigido virtuale memorizzato come BLOB di pagine nell'archivio.
* **Disco temporaneo**: macchine virtuali di Azure contengono un altro disco denominato disco temporaneo hello (etichettata come hello **D**: unità). Si tratta di un disco nel nodo hello che può essere utilizzato per l'area scratch.
* **I dischi dati**: È anche possibile collegare dischi aggiuntivi tooyour virtual machine come dischi dati e verranno archiviati nel servizio di archiviazione come BLOB di pagine.

Hello nelle sezioni seguenti vengono descritti consigli per l'utilizzo di questi dischi diversi.

### <a name="operating-system-disk"></a>Disco del sistema operativo

Per disco del sistema operativo si intende un disco rigido virtuale che è possibile avviare e montare come versione in esecuzione di un sistema operativo ed è etichettato come unità **C** .

Valore predefinito di memorizzazione nella cache dei criteri nel disco del sistema operativo hello è **lettura/scrittura**. Per applicazioni sensibili delle prestazioni, è consigliabile usare dischi dati anziché disco del sistema operativo hello. Nella sezione hello nei dischi di dati sottostante.

### <a name="temporary-disk"></a>Disco temporaneo

unità di archiviazione temporanea, etichettata come hello Hello **D**: disco, non è persistente tooAzure nell'archiviazione blob. Non archiviare il file del database utente o un file di log delle transazioni utente in hello **D**: unità.

Per la serie D Dv2 serie e le macchine virtuali serie G, unità temporanea di hello su queste macchine virtuali è basata su SSD. Se il carico di lavoro utilizza in modo intensivo del database TempDB (ad esempio per gli oggetti temporanei o join complessi), l'archiviazione di TempDB in hello **D** unità potrebbe causare una velocità effettiva di TempDB e TempDB latenza più bassa.

Per le macchine virtuali che supportano Archiviazione Premium (serie DS, DSv2 e GS), si consiglia di archiviare TempDB su un disco che supporta Archiviazione Premium con il caching di lettura attivato. Un'eccezione toothis indicazione; Se l'utilizzo di TempDB è elevato della scrittura, è possibile ottenere prestazioni più elevate archiviando TempDB in locale hello **D** unità, è inoltre basate su SSD sulle dimensioni di questi computer.

### <a name="data-disks"></a>Dischi dati

* **Utilizzare dischi dati per i file di dati e di log**: come minimo, usare l'archiviazione Premium 2 [P30 dischi](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) in un disco contiene i file di log hello e altri hello contiene dati hello e i file di TempDB. Ogni disco di archiviazione Premium fornisce una serie di operazioni IOPs e la larghezza di banda (MB/s) a seconda delle dimensioni, come descritto nell'articolo seguente hello: [con archiviazione Premium per i dischi](../../../storage/common/storage-premium-storage.md).

* **Striping del disco**: per una maggiore velocità effettiva, è possibile aggiungere ulteriori dischi dati e usare lo striping del disco. numero di hello toodetermine di dischi dati, è necessario tooanalyze hello svariate e larghezza di banda necessaria per i file di log e per i dati e i file di TempDB. Si noti che diverse dimensioni di macchina virtuale sono diversi limiti sul numero di hello di IOPs e la larghezza di banda supportate, vedere le tabelle di hello in IOPS per [dimensioni della macchina virtuale](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Utilizzare hello alle linee guida:

  * Per Windows 8 e Windows Server 2012 o versione successiva, utilizzare [spazi di archiviazione](https://technet.microsoft.com/library/hh831739.aspx) con hello alle linee guida:

      1. Set hello interleave (dimensione di striping) too64 KB (65536 byte) per i carichi di lavoro OLTP e 256 KB (262.144 byte) per il data warehousing impatto sulle prestazioni di carichi di lavoro tooavoid a causa di problemi di allineamento toopartition. Questo valore deve essere impostato con PowerShell.
      1. Impostare il numero di colonne sul numero di dischi fisici. Usare PowerShell (e non l'interfaccia utente di Server Manager) per configurare più di 8 dischi. 

    Ad esempio, hello PowerShell seguente crea un nuovo pool di archiviazione con hello interleave dimensioni too64 KB e hello il numero di colonne too2:

    ```powershell
    $PoolCount = Get-PhysicalDisk -CanPool $True
    $PhysicalDisks = Get-PhysicalDisk | Where-Object {$_.FriendlyName -like "*2" -or $_.FriendlyName -like "*3"}

    New-StoragePool -FriendlyName "DataFiles" -StorageSubsystemFriendlyName "Storage Spaces*" -PhysicalDisks $PhysicalDisks | New-VirtualDisk -FriendlyName "DataFiles" -Interleave 65536 -NumberOfColumns 2 -ResiliencySettingName simple –UseMaximumSize |Initialize-Disk -PartitionStyle GPT -PassThru |New-Partition -AssignDriveLetter -UseMaximumSize |Format-Volume -FileSystem NTFS -NewFileSystemLabel "DataDisks" -AllocationUnitSize 65536 -Confirm:$false 
    ```

  * Per Windows 2008 R2 o versioni precedenti, è possibile utilizzare i dischi dinamici (volumi con striping OS) e la dimensione di striping hello è sempre 64 KB. Si noti che questa opzione è deprecata a partire da Windows 8 e Windows Server 2012. Per informazioni, vedere l'istruzione di supporto hello in [servizio dischi virtuali viene effettuata la transizione tooWindows API di gestione archiviazione](https://msdn.microsoft.com/library/windows/desktop/hh848071.aspx).

  * Se il carico di lavoro non usa in modo intensivo i log e non sono necessarie operazioni di input/output al secondo dedicate, è possibile configurare un solo pool di archiviazione. In caso contrario, creare due pool di archiviazione, uno per i file di log hello e un altro pool di archiviazione per i file di dati hello e TempDB. Determinare il numero di hello di dischi associati a ogni pool di archiviazione in base alle proprie aspettative di carico. Tenere presente che le diverse dimensioni di macchine virtuali consentono diversi numeri di dischi dati associati. Per altre informazioni, vedere [Dimensioni delle macchine virtuali in Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

  * Se non si utilizza l'archiviazione Premium (scenari di sviluppo/test), indicazione hello è numero massimo di hello tooadd di dischi di dati supportati dal [dimensioni delle macchine Virtuali](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e utilizzare lo Striping del disco.

* **Criteri di memorizzazione nella cache**: i dischi di dati per l'archiviazione Premium, abilitare la cache di lettura sui dischi dati hello ospita solo il file di dati e di TempDB. Se non si usa Archiviazione Premium, non abilitare la memorizzazione nella cache per i dischi dati. Per istruzioni su come configurare la cache del disco, vedere hello seguenti argomenti: [Set-AzureOSDisk](https://msdn.microsoft.com/library/azure/jj152847) e [Set-AzureDataDisk](https://msdn.microsoft.com/library/azure/jj152851.aspx).

  > [!WARNING]
  > Arrestare il servizio di SQL Server hello quando si modifica l'impostazione della cache di hello della macchina virtuale di Azure dischi tooavoid hello probabilità eventuali danneggiamenti del database.

* **Dimensioni dell'unità di allocazione NTFS**: quando si formatta il disco di dati hello, si consiglia di utilizzare una dimensione di unità di allocazione di 64 KB per file di dati e di log, nonché di TempDB.

* **Procedure consigliate di gestione del disco**: quando si digita la rimozione di un disco dati o modificare la cache, è possibile arrestare il servizio di SQL Server hello durante la modifica di hello. Quando le impostazioni di memorizzazione nella cache di hello sono modificato sul disco del sistema operativo hello, Azure arresta hello VM cambia il tipo di cache di hello e riavvia hello VM. Quando vengono modificate le impostazioni della cache di hello di un disco dati, hello VM non è stato arrestato, ma il disco di dati hello viene disconnesso da hello VM hello durante la modifica e il successivo ricollegamento.

  > [!WARNING]
  > Hello toostop errore del servizio SQL Server durante queste operazioni può causare il danneggiamento del database.

## <a name="io-guidance"></a>Linee guida per l'I/O

* Quando si parallelizza dell'applicazione e le richieste, vengono ottenuti i risultati di migliore Hello con archiviazione Premium. Archiviazione Premium è progettato per scenari in cui la profondità della coda i/o hello è maggiore di 1, in modo che le minime o alcun miglioramento delle prestazioni per le richieste di seriale a thread singolo (anche se sono con utilizzo intensivo di archiviazione). Ad esempio, ciò potrebbe influire sulla di risultati dei test a thread singolo hello di strumenti di analisi delle prestazioni, ad esempio SQLIO.

* È consigliabile usare la [compressione di pagina del database](https://msdn.microsoft.com/library/cc280449.aspx) in quanto consente di migliorare le prestazioni dei carichi di lavoro con utilizzo intensivo di I/O. Tuttavia, la compressione dei dati di hello potrebbe aumentare l'utilizzo della CPU nel server di database hello hello.

* Considerare l'attivazione immediata dei file inizializzazione tooreduce hello tempo necessario per l'allocazione iniziale di file. Il vantaggio di tootake dell'inizializzazione immediata dei file, concedere hello account del servizio SQL Server (MSSQLSERVER) SE_MANAGE_VOLUME_NAME e aggiungerlo toohello **eseguire attività di manutenzione Volume** criteri di sicurezza. Se si utilizza un'immagine della piattaforma SQL Server per Azure, account del servizio predefinito hello (NT Service\MSSQLSERVER) non verrà aggiunto toohello **eseguire attività di manutenzione Volume** criteri di sicurezza. In altre parole, l'inizializzazione file immediata non è abilitata in un'immagine della piattaforma Server SQL di Azure. Dopo l'aggiunta di hello SQL Server service account toohello **eseguire attività di manutenzione Volume** criteri di protezione, riavviare il servizio SQL Server hello. Potrebbero essere presenti indicazioni sulla sicurezza da considerare per l'utilizzo di questa funzionalità. Per altre informazioni, vedere [Inizializzazione di file di database](https://msdn.microsoft.com/library/ms175935.aspx).

* **aumento automatico delle dimensioni** viene considerato toobe una semplice contingenza per la crescita imprevista. La crescita dei dati e dei log non viene gestita quotidianamente con l'aumento automatico delle dimensioni. Se viene usata, pre-aumento delle dimensioni file hello utilizzando l'opzione Size hello.

* Assicurarsi che **autoshrink** è disabilitato tooavoid inutili sovraccarichi che possono influire negativamente sulle prestazioni.

* Spostare tutti i dischi toodata database, inclusi i database di sistema. Per altre informazioni vedere l'articolo [Spostare i database di sistema](https://msdn.microsoft.com/library/ms345408.aspx).

* Spostare l'errore log e trace file directory toodata dischi del Server SQL. È possibile farlo in Gestione configurazione SQL Server facendo clic con il pulsante destro del mouse sull'istanza di SQL Server e selezionando Proprietà. Hello impostazioni di file registro e di traccia di errore possono essere modificate in hello **parametri di avvio** hello scheda Dump Directory specificata nella hello **avanzate** hello scheda schermata seguente viene illustrato dove toolook per parametro di avvio Registro errore Hello.

    ![Schermata del log degli errori di SQL](./media/virtual-machines-windows-sql-performance/sql_server_error_log_location.png)

* Configurare il percorso predefinito del file di backup e del file di database. Usare i suggerimenti di hello in questo argomento e apportare modifiche di hello nella finestra proprietà di Server hello. Per istruzioni, vedere [hello visualizzare o modificare percorsi predefiniti per i dati e i file di Log (SQL Server Management Studio)](https://msdn.microsoft.com/library/dd206993.aspx). Hello schermata riportata di seguito viene illustrato dove toomake queste modifiche.

    ![File di log e di backup di SQL](./media/virtual-machines-windows-sql-performance/sql_server_default_data_log_backup_locations.png)
* Abilita bloccato tooreduce pagine i/o e qualsiasi attività di paging. Per ulteriori informazioni, vedere [abilitare hello Lock Pages in Memory-opzione (Windows)](https://msdn.microsoft.com/library/ms190730.aspx).

* Se si esegue SQL Server 2012, installare l'aggiornamento cumulativo 10 del Service Pack 1. Questo aggiornamento contiene correzione hello per ridurre le prestazioni dei / o quando si esegue select nell'istruzione di tabella temporanea in SQL Server 2012. Per altre informazioni, vedere questo [articolo della Knowledge Base](http://support.microsoft.com/kb/2958012).

* È consigliabile comprimere i file di dati durante il trasferimento in entrata e in uscita di Azure.

## <a name="feature-specific-guidance"></a>Linee guida per le specifiche della funzione

Alcune distribuzioni possono ottenere ulteriori miglioramenti delle prestazioni usando tecniche di configurazione più avanzate. Hello seguito sono riportate alcune funzionalità di SQL Server che consentono di ottenere prestazioni migliori tooachieve:

* **Eseguire il backup archiviazione tooAzure**: quando si eseguono backup per SQL Server in esecuzione in macchine virtuali di Azure, è possibile utilizzare [tooURL di Backup di SQL Server](https://msdn.microsoft.com/library/dn435916.aspx). Questa funzionalità è disponibile a partire da SQL Server 2012 SP1 CU2 e consigliati per il backup dei dischi dati toohello associata. Quando si backup/ripristino in/da archiviazione di Azure, seguire indicazioni hello disponibili in [Backup di SQL Server tooURL procedure consigliate e risoluzione dei problemi e ripristino da backup archiviati in archiviazione di Azure](https://msdn.microsoft.com/library/jj919149.aspx). È anche possibile automatizzare i backup usando [Backup automatizzato per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-automated-backup.md).

    TooSQL precedente Server 2012, è possibile utilizzare [Backup di SQL Server tooAzure strumento](https://www.microsoft.com/download/details.aspx?id=40740). Questo strumento consente di velocità effettiva del backup tooincrease utilizzando più destinazioni di backup in striping.

* **File di dati di SQL Server in Azure**: questa nuova funzionalità ( [file di dati di SQL Server in Azure](https://msdn.microsoft.com/library/dn385720.aspx)) è disponibile a partire da SQL Server 2014. L'esecuzione di SQL Server con file di dati in Azure dimostra le caratteristiche di prestazioni paragonabili a quelle dei dischi dati di Azure.

## <a name="next-steps"></a>Passaggi successivi

Per le procedure consigliate relative alla sicurezza, vedere [Considerazioni relative alla sicurezza per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-security.md).

Esaminare altri argomenti relativi alle macchine virtuali di SQL Server in [Panoramica di SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).
