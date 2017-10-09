# <a name="azure-managed-disks-overview"></a>Panoramica di Azure Managed Disks

I dischi di Azure gestiti semplifica la gestione disco per le macchine virtuali IaaS di Azure hello [gli account di archiviazione](../articles/storage/common/storage-introduction.md) associati hello dischi di macchina virtuale. È necessario solo il tipo di hello toospecify ([Premium](../articles/storage/common/storage-premium-storage.md) o [Standard](../articles/storage/common/storage-standard-storage.md)) e le dimensioni di hello del disco è necessario, Azure crea e gestisce disco hello per l'utente.

## <a name="benefits-of-managed-disks"></a>Vantaggi dei dischi gestiti

Esaminiamo un alcuni dei vantaggi di hello è possibile ottenere utilizzando dischi gestiti, a partire da questo video di Channel 9, [resilienza migliore macchina virtuale di Azure con dischi gestiti](https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency).
<br/>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency/player]

### <a name="simple-and-scalable-vm-deployment"></a>Distribuzione semplice e scalabile di macchine virtuali

Per gestire archiviazione handle dischi background hello. In precedenza, era toocreate account toohold hello i dischi di archiviazione (file VHD) per le macchine virtuali di Azure. La scalabilità, è necessario toomake che creato gli account di archiviazione aggiuntive si non supera il limite di IOPS hello per l'archiviazione con uno qualsiasi dei dischi. Con dischi gestiti gestione archiviazione, non è limitato da hello limiti dell'account di archiviazione (ad esempio 20.000 IOPS / account). Inoltre non è più necessario toocopy gli account di archiviazione toomultiple immagini personalizzate (file VHD). È possibile gestirli in una posizione centrale: un account di archiviazione per ogni area di Azure e usarli toocreate centinaia di macchine virtuali in una sottoscrizione.

Dischi gestiti consentirà toocreate backup too10, VM 000 **dischi** in una sottoscrizione, che verrà consentono toocreate migliaia di **macchine virtuali** in una singola sottoscrizione. Anche questa funzionalità aumenta la scalabilità hello di [set di scalabilità macchina virtuale (VMSS)](../articles/virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) consentendo toocreate le VM tooa delle migliaia in un VMSS utilizzando un'immagine del Marketplace.

### <a name="better-reliability-for-availability-sets"></a>Maggiore affidabilità per i set di disponibilità

Dischi gestiti garantisce maggiore affidabilità per set di disponibilità, assicurando che hello dischi di [macchine virtuali in un Set di disponibilità](../articles/virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) sufficientemente isolate tra di loro tooavoid singoli punti di errore. Ciò avviene inserendo automaticamente i dischi hello in unità di scala di archiviazione diversi (timbri). Se un timbro non riesce a causa di un errore toohardware o software, non solo hello istanze di macchina virtuale con dischi in tali timbri. Si supponga, ad esempio, si dispone di un'applicazione in esecuzione in cinque macchine virtuali e macchine virtuali hello si trovino in un Set di disponibilità. Hello dischi per tali macchine virtuali non verranno tutte essere archiviati in hello stesso timestamp, in modo che se uno stamp diventa inattiva, hello altre istanze di un'applicazione hello continuano toorun.

### <a name="highly-durable-and-available"></a>Elevati livelli di durabilità e disponibilità

I dischi di Azure sono stati progettati per il 99,999% di disponibilità. È possibile quindi riposare serenamente sapendo di avere tre repliche dei dati, che consentono una durabilità elevata. Se le repliche di uno o due anche problemi, le repliche rimanenti hello garantiscono la persistenza dei dati ed elevata tolleranza agli errori. Questa architettura ha consentito ad Azure di offrire costantemente durabilità di livello aziendale per i dischi IaaS, con una percentuale di frequenza errori annualizzata pari a ZERO, la migliore del settore. 

### <a name="granular-access-control"></a>Controllo di accesso granulare

È possibile utilizzare [gestire accesso controllo (RBAC)](../articles/active-directory/role-based-access-control-what-is.md) tooassign autorizzazioni specifiche per un tooone disco gestito o di altri utenti. Gestito dischi espone un'ampia gamma di operazioni, tra cui lettura, scrittura (creazione/aggiornamento), eliminazione e il recupero di un [firma di accesso condiviso (SAS) URI](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md) per disco hello. È possibile concedere accesso tooonly hello operazioni che è necessario disporre di tooperform proprio lavoro. Ad esempio, se non si desidera un toocopy di persona, un account di archiviazione tooa disco gestito, è possibile scegliere di non toogrant accesso toohello azione Esporta per quel disco gestito. Analogamente, se non si desidera un toouse persona un toocopy URI SAS un disco gestito, è possibile scegliere non toogrant toohello tale autorizzazione disco gestito.

### <a name="azure-backup-service-support"></a>Supporto del servizio Backup di Azure
Utilizzare il servizio di Backup di Azure con dischi gestiti toocreate un processo di backup con backup basate sul tempo, facilmente ripristinati VM e i criteri di conservazione dei backup. Dischi gestiti supportano solo l'archiviazione con ridondanza locale (LRS) come opzione di replica hello. Ciò significa che mantiene tre copie dei dati hello all'interno di una singola area. Per eseguire il ripristino di emergenza dell'area, è necessario eseguire il backup dei dischi delle macchine virtuali in un'altra area usando il [servizio Backup di Azure](../articles/backup/backup-introduction-to-azure-backup.md) e un account di archiviazione con ridondanza geografica come insieme di credenziali di backup. Backup di Azure supporta attualmente le dimensioni dei dischi dati backup too1TB per il backup. Per altre informazioni in merito, vedere la sezione relativa all'[uso del servizio Backup di Azure per macchine virtuali con dischi gestiti](../articles/backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="pricing-and-billing"></a>Prezzi e fatturazione

Quando si usano dischi gestiti, si applica hello fatturazione considerazioni seguenti:
* Tipo di archiviazione

* Dimensione disco

* Numero di transazioni

* Trasferimenti di dati in uscita

* Snapshot del disco gestito (copia dell'intero disco)

Tali considerazioni vengono ora esaminate più in dettaglio.

**Tipo di archiviazione:** Managed Disks offre due livelli di prestazioni, [Premium](../articles/storage/common/storage-premium-storage.md), basato su unità SSD, e [Standard](../articles/storage/common/storage-standard-storage.md), basato su unità disco rigido. la fatturazione di un disco gestito Hello dipende il tipo di archiviazione selezionato per il disco di hello.


**Dimensioni del disco**: fatturazione per i dischi gestiti dipende dalle dimensioni hello il provisioning del disco hello. Mappe Azure hello toohello dimensioni provisioning (arrotondata per eccesso) più vicino di opzione di dischi gestiti come specificato hello seguito nelle tabelle. Ogni tooone mappe disco gestito di hello supportate le dimensioni di provisioning e viene fatturato di conseguenza. Ad esempio, se si crea un disco gestito standard e specificare una dimensione pari a 200 GB provisioning, verrà addebitato in base ai prezzi hello del tipo di disco S20 hello.

Di seguito sono riportate le dimensioni dei dischi hello disponibili per un disco gestito premium:

| **Tipo di disco <br>gestito Premium** | **P4** | **P6** |**P10** | **P20** | **P30** | **P40** | **P50** | 
|------------------|---------|---------|---------|---------|----------------|----------------|----------------|  
| Dimensione disco        | 32 GB   | 64 GB   | 128 GB  | 512 GB  | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


Di seguito sono riportate le dimensioni dei dischi hello disponibili per un disco gestito standard:

| **Tipo di disco <br>gestito Standard** | **S4** | **S6** | **S10** | **S20** | **S30** | **S40** | **S50** |
|------------------|---------|---------|--------|--------|----------------|----------------|----------------| 
| Dimensione disco        | 32 GB   | 64 GB   | 128 GB | 512 GB | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


**Numero di transazioni**: verrà addebitato per il numero di transazioni eseguite su un disco gestito standard hello. Non sono previsti costi per le transazioni per un disco gestito Premium.

**Trasferimenti di dati in uscita**: i [trasferimenti di dati in uscita](https://azure.microsoft.com/pricing/details/data-transfers/) (dati in uscita dai data center di Azure) vengono fatturati in base all'uso della larghezza di banda.

Per informazioni dettagliate sui prezzi di Managed Disks, vedere [Prezzi di Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks).


## <a name="managed-disk-snapshots"></a>Snapshot dei dischi gestiti

Uno snapshot gestito è una copia di sola lettura di un disco gestito che viene archiviata come disco gestito Standard per impostazione predefinita. Gli snapshot permettono di eseguire il backup dei dischi gestiti in qualsiasi momento. Queste istantanee esistono indipendentemente da disco di origine hello e possono essere utilizzato toocreate nuovi dischi gestiti. Vengano loro addebitate in base alle dimensioni hello utilizzato. Ad esempio, se si crea uno snapshot di un disco gestito con dimensioni effettive dei dati utilizzate di 10 GB e la capacità di provisioning di 64 GB, snapshot verrà addebitato solo per le dimensioni di hello utilizzato dati di 10 GB.  

[Snapshot incrementali](../articles/virtual-machines/windows/incremental-snapshots.md) non sono attualmente supportate per i dischi gestiti, ma sarà supportato in hello future.

toolearn altre informazioni sulla modalità snapshot toocreate con dischi gestiti, verificare queste risorse:

* [Creare una copia del disco rigido virtuale archiviato come disco gestito usando gli snapshot in Windows](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)
* [Creare una copia del disco rigido virtuale archiviato come disco gestito usando gli snapshot in Linux](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)


## <a name="images"></a>Immagini

Managed Disks supporta anche la creazione di un'immagine personalizzata gestita. È possibile creare un'immagine dal disco rigido virtuale personalizzato in un account di archiviazione oppure direttamente da una macchina virtuale (preparata con Sysprep) generalizzata. Acquisisce in una singola immagine tutti i dischi associati a una macchina virtuale, inclusi sia hello del sistema operativo e i dischi di dati gestiti. Questo consente la creazione di centinaia di macchine virtuali con l'immagine personalizzata senza hello necessario toocopy o gestire gli account di archiviazione.

Per informazioni sulla creazione di immagini, estrarre hello seguenti articoli:
* [Come toocapture un'immagine gestita di una macchina virtuale generalizzata in Azure](../articles/virtual-machines/windows/capture-image-resource.md)
* [Come toogeneralize e acquisire una macchina virtuale Linux utilizzando hello Azure CLI 2.0](../articles/virtual-machines/linux/capture-image.md)

## <a name="images-versus-snapshots"></a>Immagini e snapshot

Spesso vedere parola hello "immagine" utilizzata con le macchine virtuali e ora "snapshot" nonché. È importante toounderstand differenza di hello tra questi. Managed Disks permette di acquisire l'immagine di una macchina virtuale generalizzata che è stata deallocata. Questa immagine includerà tutti i dischi collegati di hello toohello macchina virtuale. È possibile utilizzare questo toocreate immagine una nuova macchina virtuale e che include tutti i dischi di hello.

Uno snapshot è una copia di un disco in hello punto nel tempo, che questa viene eliminata. Si applica solo tooone disco. Se si dispone di una macchina virtuale che dispone solo di un disco (Buongiorno del sistema operativo), è possibile richiedere uno snapshot o un'immagine di esso e creare una macchina virtuale da snapshot hello o immagine hello.

La situazione cambia se la macchina virtuale include cinque dischi con striping. È Impossibile creare uno snapshot di ciascuno dei dischi hello, ma non esiste alcuna informazione all'interno di hello VM dello stato di hello di dischi hello: snapshot hello riconosce solo un disco. In questo caso, gli snapshot hello sarebbe necessario toobe coordinate tra loro e che non è attualmente supportato.

## <a name="managed-disks-and-encryption"></a>Managed Disks e crittografia

Esistono due tipi di crittografia toodiscuss dischi toomanaged di riferimento. Hello uno viene innanzitutto archiviazione servizio di crittografia (SSE), che viene eseguita dal servizio di archiviazione hello. Hello seconda è la crittografia su disco di Azure, che è possibile attivare su hello del sistema operativo e i dischi dati per le macchine virtuali.

### <a name="storage-service-encryption-sse"></a>Crittografia del servizio di archiviazione di Azure (SSE)

[La crittografia del servizio di archiviazione Azure](../articles/storage/common/storage-service-encryption.md) fornisce la crittografia a riposo e proteggere il toomeet dati propri impegni aziendali di conformità e sicurezza. SSE è abilitata per impostazione predefinita per tutti i dischi gestiti, gli snapshot e le immagini in tutte le aree di hello in cui i dischi gestiti è disponibile. Inizio il 10 giugno 2017, tutti nuovi gestiti snapshot/dischi o immagini e dischi gestiti tooexisting nuovi dati vengono automaticamente crittografati a riposo con le chiavi gestite da Microsoft.  Visitare hello [pagina delle domande frequenti di dischi gestiti](../articles/virtual-machines/windows/faq-for-disks.md#managed-disks-and-storage-service-encryption) per altri dettagli.


### <a name="azure-disk-encryption-ade"></a>Crittografia dischi di Azure (ADE)

Crittografia disco Azure consente tooencrypt hello del sistema operativo e i dischi di dati utilizzati da una macchina virtuale IaaS. Sono inclusi i dischi gestiti. Per Windows, hello unità vengono crittografate mediante la tecnologia di crittografia BitLocker standard del settore. Per Linux, dischi hello vengono crittografati mediante la tecnologia hello Crypt di data mining. Questo è integrato con insieme credenziali chiavi Azure tooallow è toocontrol e gestire chiavi di crittografia disco hello. Per altre informazioni, vedere [Crittografia dischi di Azure per macchine virtuali IaaS Windows e Linux](../articles/security/azure-security-disk-encryption.md).

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui dischi gestiti, vedere toohello seguenti articoli.

### <a name="get-started-with-managed-disks"></a>Informazioni di base sui Dischi gestiti

* [Creare una VM con Resource Manager e PowerShell](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm.md)

* [Creare una VM Linux di hello Azure CLI 2.0](../articles/virtual-machines/linux/quick-create-cli.md)

* [Collegare un tooa disco dati gestiti macchina virtuale di Windows con PowerShell](../articles/virtual-machines/windows/attach-disk-ps.md)

* [Aggiungere una VM Linux di tooa disco gestito](../articles/virtual-machines/linux/add-disk.md)

* [Script di esempio di PowerShell di Managed Disks](https://github.com/Azure-Samples/managed-disks-powershell-getting-started)

* [Usare Managed Disks nei modelli di Azure Resource Manager](../articles/virtual-machines/windows/using-managed-disks-template-deployments.md)

### <a name="compare-managed-disks-storage-options"></a>Confronto tra le opzioni di archiviazione di Managed Disks

* [Dischi e Archiviazione Premium](../articles/storage/common/storage-premium-storage.md)

* [Dischi e Archiviazione Standard](../articles/storage/common/storage-standard-storage.md)

### <a name="operational-guidance"></a>Informazioni operative

* [Eseguire la migrazione da altre piattaforme e AWS tooManaged dischi in Azure](../articles/virtual-machines/windows/on-prem-to-azure.md)

* [Convertire i dischi di macchine virtuali di Azure toomanaged in Azure](../articles/virtual-machines/windows/migrate-to-managed-disks.md)
