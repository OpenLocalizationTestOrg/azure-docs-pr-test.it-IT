
## <a name="about-vhds"></a>Informazioni sui dischi rigidi virtuali

Hello dischi rigidi virtuali usati in Azure sono file con estensione vhd archiviati come BLOB di pagine in un account di archiviazione standard o premium di Azure. Per ulteriori dettagli sui BLOB di pagine, vedere [Informazioni sui BLOB in blocchi e sui BLOB di pagine](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs/). Per informazioni su Archiviazione Premium, vedere l'articolo relativo alle [prestazioni elevate di Archiviazione Premium e macchine virtuali di Azure](../articles/storage/common/storage-premium-storage.md).

Azure supporta hello disco in formato VHD fissato. getta formato fissata Hello hello disco logico out in modo lineare all'interno di file hello, in modo tale offset del disco X venga archiviato all'offset del blob X. Un piccolo piè di pagina alla fine di hello del blob hello vengono descritte le proprietà di hello di hello disco rigido virtuale. Spesso, formato fisso hello comporta uno spreco di spazio poiché la maggior parte dei dischi sono presenti intervalli inutilizzati di grandi dimensioni in essi contenuti. Tuttavia, Azure archivia i file con estensione vhd in un formato di tipo sparse, pertanto si ottengono vantaggi hello di entrambi hello fisso e dischi dinamici in hello stesso tempo. Per ulteriori dettagli, vedere [Introduzione ai dischi rigidi virtuali](https://technet.microsoft.com/library/dd979539.aspx).

Tutti i file con estensione vhd in Azure che si desidera toouse come disco di origine toocreate o immagini sono di sola lettura. Quando si crea un'immagine o un disco, Azure esegue copie di hello file con estensione vhd. Queste copie possono essere di sola lettura o lettura e scrittura, a seconda della modalità di utilizzo hello disco rigido virtuale.

Quando si crea una macchina virtuale da un'immagine, Azure crea un disco per la macchina virtuale hello che è una copia del file con estensione vhd di origine hello. tooprotect l'eliminazione involontaria, tramite Azure viene inserito un lease in qualsiasi file con estensione vhd di origine che ha utilizzato toocreate un'immagine, un disco del sistema operativo o un disco dati.

Prima di poter eliminare un file con estensione vhd di origine, è necessario lease hello tooremove eliminando hello disco o l'immagine. toodelete un file con estensione vhd utilizzato da una macchina virtuale come disco del sistema operativo, è possibile eliminare macchina virtuale hello disco del sistema operativo hello e file con estensione vhd di origine hello in un'unica macchina virtuale hello di eliminazione e l'eliminazione di tutti i dischi associati. Tuttavia, l'eliminazione di un file con estensione vhd che rappresenta l'origine di un disco dati richiede l'esecuzione di diversi passaggi in un determinato ordine: Innanzitutto si scollega disco hello dalla macchina virtuale hello, quindi Elimina hello disco e quindi eliminare il file con estensione vhd di hello.

> [!WARNING]
> Se si elimina un file con estensione .vdh di origine dalla memoria o l'account di archiviazione, Microsoft non può recuperare tali dati.
> 

## <a name="types-of-disks"></a>Tipi di dischi 

I dischi di Azure sono stati progettati per il 99,999% di disponibilità. I dischi di Azure hanno offerto in modo costante una durabilità di livello aziendale, con una percentuale di frequenza di errori annualizzata pari a ZERO, ovvero la migliore del settore.

Durante la creazione di dischi è possibile scegliere tra due livelli di prestazioni per l'archiviazione: Archiviazione Standard e Archiviazione Premium. I dischi possono essere di due tipi, gestiti e non gestiti, e possono risiedere in entrambi i livelli di prestazioni.


### <a name="standard-storage"></a>Archiviazione standard 

Archiviazione Standard è supportata da unità disco rigido e offre un'archiviazione conveniente con buone prestazioni. Per Archiviazione Standard è possibile scegliere tra archiviazione replicata in locale in un data center o con ridondanza geografica con i data center primario e secondario. Per altre informazioni sulla replica dell'archiviazione, vedere [Replica di Archiviazione di Azure](../articles/storage/common/storage-redundancy.md). 

Per altre informazioni sull'uso di Archiviazione Standard con dischi di macchina virtuale, vedere l'articolo relativo ad [Archiviazione Standard e dischi](../articles/storage/common/storage-standard-storage.md).

### <a name="premium-storage"></a>Archiviazione Premium 

Archiviazione Premium è supportata da unità SSD e offre prestazioni elevate e supporto per dischi a bassa latenza per le macchine virtuali che eseguono carichi di lavoro con elevato numero di operazioni di I/O. È possibile usare Archiviazione Premium con macchine virtuali di Azure serie DS, DSv2, GS, Ls o FS. Per altre informazioni, vedere [Archiviazione Premium](../articles/storage/common/storage-premium-storage.md).

### <a name="unmanaged-disks"></a>Dischi non gestiti

I dischi non gestiti sono tipo tradizionale di hello di dischi che sono stati usati dalle macchine virtuali. Queste operazioni, si crea il proprio account di archiviazione e specificare l'account di archiviazione quando si crea il disco di hello. Si dispone di toomake che non si inserisce un numero eccessivo di dischi hello stesso account di archiviazione, poiché si può superare hello [obiettivi di scalabilità](../articles/storage/common/storage-scalability-targets.md) hello dell'account di archiviazione (ad esempio 20.000 IOPS), comportando hello macchine virtuali limitate. Con i dischi non gestiti, è necessario toofigure toomaximize hello utilizzare di uno o più storage account tooget hello migliori prestazioni con le macchine virtuali.

### <a name="managed-disks"></a>Dischi gestiti 

Gestire gli handle di dischi di archiviazione hello creazione/gestione sfondo hello degli account per l'utente e garantisce che non si dispone tooworry sui limiti di scalabilità hello hello dell'account di archiviazione. È sufficiente specificare dimensioni del disco hello e il livello di prestazioni hello (Standard o Premium) e Azure crea e gestisce disco hello per l'utente. Anche se si aggiungono dischi o applicare la scalabilità verticale hello VM, non è tooworry sull'archiviazione hello in uso. 

È anche possibile gestire immagini personalizzate in un account di archiviazione per ogni area di Azure e usarli toocreate centinaia di macchine virtuali in hello stessa sottoscrizione. Per ulteriori informazioni sui dischi gestiti, vedere hello [Panoramica di dischi gestiti](../articles/virtual-machines/windows/managed-disks-overview.md).

È consigliabile usare dischi gestiti di Azure per nuove macchine virtuali e convertire i dischi toomanaged dischi non gestito precedente, tootake sfruttare hello numerose funzionalità disponibili nei dischi gestiti.

### <a name="disk-comparison"></a>Confronto dei dischi

Hello nella tabella seguente fornisce un confronto tra Visual Studio Premium Standard per entrambi non gestito e gestito si decide quali toouse toohelp di dischi.

|    | Disco Premium di Azure | Disco Standard di Azure |
|--- | ------------------ | ------------------- |
| Tipo di disco | Unità a stato solido (SSD) | Unità disco rigido (HDD)  |
| Panoramica  | Supporto per dischi SSD a prestazioni elevate e bassa latenza per le macchine virtuali che eseguono carichi di lavoro con elevato numero di operazioni di I/O o ambienti di produzione host cruciali | Supporto per dischi HDD convenienti per scenari di macchine virtuali di sviluppo e test |
| Scenario  | Carichi di lavoro di produzione su cui influiscono le prestazioni | Sviluppo e test, non critico, <br>ad accesso non frequente |
| Dimensione disco | P4: 32 GB (solo Managed Disks)<br>P6: 64 GB (solo Managed Disks)<br>P10: 128 GB<br>P20: 512 GB<br>P30: 1024 GB<br>P40: 2048 GB<br>P50: 4095 GB | Dischi non gestiti: tra 1 GB e 4 TB (4095 GB) <br><br>Dischi gestiti:<br> S4: 32 GB <br>S6: 64 GB <br>S10: 128 GB <br>S20: 512 GB <br>S30: 1024 GB <br>S40: 2048 GB<br>S50: 4095 GB| 
| Velocità effettiva massima per disco | 250 MB/s | 60 MB/s | 
| Numero massimo di operazioni di I/O al secondo per disco | 7500 IOPS | 500 IOPS | 

