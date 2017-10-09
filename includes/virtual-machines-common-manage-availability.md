## <a name="understand-vm-reboots---maintenance-vs-downtime"></a>Informazioni sui riavvii delle VM: manutenzione e tempo di inattività
Esistono tre scenari che possono causare la macchina toovirtual in Azure influenzate: manutenzione dell'hardware non pianificato, tempo di inattività imprevisto e la manutenzione pianificata.

* **Evento di manutenzione non pianificata Hardware** si verifica quando hello piattaforma Azure consente di stimare hardware hello o qualsiasi piattaforma tooa associato fisico computer del componente, sta toofail. Quando la piattaforma hello viene stimato un errore, rilascia un hardware non pianificato manutenzione evento tooreduce hello impatto toohello macchine virtuali ospitate su tale hardware. Azure Usa hello toomigrate tecnologia di migrazione in tempo reale le macchine virtuali da hello errori hardware tooa integro del computer fisico. Migrazione in tempo reale è una macchina virtuale operazione che solo le pause hello macchina virtuale per un breve periodo di mantenimento. Memoria, i file aperti e connessioni di rete vengono mantenute, ma le prestazioni potrebbero risultare ridotte prima e/o dopo l'evento hello. Nei casi in cui non è possibile utilizzare Live Migration, hello VM subiranno tempi di inattività imprevisti, come descritto di seguito.


* **Un tempo di inattività imprevisti** raramente si verifica quando si è verificato un errore hardware hello o hello dell'infrastruttura sottostante la macchina virtuale in qualche modo. Può trattarsi, ad esempio, di errori della rete locale, guasti di un disco locale o altri errori a livello di rack. Quando viene rilevato un errore di questo tipo, hello piattaforma Azure esegue automaticamente la migrazione (heals) il computer fisico integro macchina virtuale tooa. Durante la procedura di correzione di hello, macchine virtuali verificarsi tempi di inattività (riavvio) e la perdita di alcuni casi di unità temporanea hello. Hello collegati del sistema operativo e i dischi dati vengono sempre mantenuti. 

* **Eventi di manutenzione pianificato** sono aggiornamenti periodici eseguiti da Microsoft toohello tooimprove piattaforma Azure sottostante l'affidabilità complessive, prestazioni e protezione dell'infrastruttura della piattaforma hello le macchine virtuali eseguite in. La maggior parte di questi aggiornamenti viene eseguita senza alcuna conseguenza per le macchine virtuali o i servizi cloud. Vedere [Manutenzione con mantenimento delle macchine virtuali](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/preserving-maintenance). Sebbene hello piattaforma Azure tenta toouse VM mantenimento manutenzione in tutti i casi possibili, esistono casi rari quando questi aggiornamenti richiedono il riavvio di una macchina virtuale tooapply hello gli aggiornamenti richiesti toohello infrastruttura di base. In questo caso, è possibile eseguire la manutenzione pianificata di Azure con l'operazione di ridistribuzione di manutenzione avviando manutenzione hello per le proprie macchine virtuali nella finestra di tempo appropriato hello. Per altre informazioni, vedere [Manutenzione pianificata per le macchine virtuali](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/planned-maintenance/).


impatto di hello tooreduce dei tempi di inattività dovuto tooone o più di questi eventi, è consigliabile hello consigliate di disponibilità elevata per le macchine virtuali seguenti:

* [Configurare più macchine virtuali in un set di disponibilità per la ridondanza]
* [Usare Managed Disks per le macchine virtuali nel set di disponibilità]
* [Utilizzare tooVM di risposta agli eventi pianificati tooproactively conseguenze per gli eventi] (https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-scheduled-events)
* [Configurare ogni livello dell'applicazione in set di disponibilità separati]
* [Combinare il bilanciamento del carico con set di disponibilità]

## <a name="configure-multiple-virtual-machines-in-an-availability-set-for-redundancy"></a>Configurare più macchine virtuali in un set di disponibilità per la ridondanza
applicazione di tooyour tooprovide ridondanza, si consiglia di raggruppare due o più macchine virtuali in un set di disponibilità. Questa configurazione assicura che durante un evento di manutenzione pianificato o non pianificato, almeno una macchina virtuale sia disponibile e soddisfa hello pari al 99,95% SLA di Azure. Per ulteriori informazioni, vedere hello [contratto di servizio per le macchine virtuali](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Evitare di lasciare un'unica istanza di macchina virtuale in un set di disponibilità. Le macchine virtuali in questa configurazione non si qualificano per la garanzia del contratto di servizio e sono soggette a tempi di inattività durante gli eventi di manutenzione pianificata di Azure, se non quando una macchina virtuale singola usa [Archiviazione Premium di Azure](../articles/storage/common/storage-premium-storage.md). Per singole macchine virtuali con archiviazione premium, si applica hello SLA di Azure.

Ogni macchina virtuale nel set di disponibilità viene assegnato un **dominio di aggiornamento** e **dominio di errore** da hello sottostante piattaforma Azure. Per un set di disponibilità, cinque domini di aggiornamento non configurabile dall'utente vengono assegnati per impostazione predefinita (distribuzione di gestione di risorse possono quindi essere tooprovide un aumento dei domini di aggiornamento too20) tooindicate gruppi di macchine virtuali e l'hardware fisico sottostante che può essere riavviato in hello contemporaneamente. Quando più di cinque macchine virtuali sono configurate in un unico set di disponibilità, macchina virtuale sesto hello viene inserito in hello stesso aggiornamento dominio come macchina virtuale prima di hello, hello settimo in hello che stesso dominio di aggiornamento come hello seconda macchina virtuale e pertanto in. ordine di Hello di domini di aggiornamento in corso il riavvio potrebbe non passare in modo sequenziale durante la manutenzione pianificata, ma l'aggiornamento di un solo dominio è stato riavviato alla volta. Un dominio di aggiornamento riavviato ha toorecover 30 minuti prima di manutenzione viene avviata in un dominio di aggiornamento diversi.

Domini di errore di definire il gruppo di hello di macchine virtuali che condividono un commutatore power di origine e di rete comune. Per impostazione predefinita, le macchine virtuali hello configurate all'interno del set di disponibilità sono separate tra i domini di errore toothree per le distribuzioni di gestione risorse (due domini di errore per classica). Durante l'inserimento di macchine virtuali in un set di disponibilità non protegge l'applicazione dagli errori specifici dell'applicazione o del sistema operativo, limitare l'impatto di hello di potenziali errori hardware fisico, interruzioni della rete o le interruzioni di alimentazione.

<!--Image reference-->
   ![Rappresentazione concettuale di hello aggiornamento dominio e errore di configurazione del dominio](./media/virtual-machines-common-manage-availability/ud-fd-configuration.png)

## <a name="use-managed-disks-for-vms-in-an-availability-set"></a>Usare Managed Disks per le macchine virtuali nel set di disponibilità
Se si utilizza attualmente le macchine virtuali con dischi non gestiti, è consigliabile [convertire le macchine virtuali nel Set di disponibilità di dischi gestiti di toouse](../articles/virtual-machines/windows/convert-unmanaged-to-managed-disks.md).

[Dischi gestiti](../articles/virtual-machines/windows/managed-disks-overview.md) forniscono maggiore affidabilità per set di disponibilità, verificare che i dischi di hello di macchine virtuali in un Set di disponibilità sono sufficientemente isolate una da altra tooavoid singoli punti di errore. Ciò avviene inserendo automaticamente i dischi hello nei cluster di archiviazione diverso. Se un cluster di archiviazione non riesce a causa di un errore toohardware o software, non solo hello istanze di macchina virtuale con dischi in tali timbri.

![Domini di errore dei dischi gestiti](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> numero di Hello di domini di errore per i set di disponibilità gestito varia in base a region - due o tre per ogni area. Hello nella tabella seguente mostra il numero di hello per area

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

Se si prevede di macchine virtuali toouse con [non gestita dischi](../articles/virtual-machines/windows/about-disks-and-vhds.md#types-of-disks), di seguito sono riportati le procedure consigliate per gli account di archiviazione in cui vengono archiviati i dischi rigidi virtuali (VHD) di macchine virtuali come [BLOB di pagine](https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs#about-page-blobs).

1. **Mantenere tutti i dischi (sistema operativo e dati) associati a una macchina virtuale in hello stesso account di archiviazione**
2. **Hello revisione [limiti](../articles/storage/common/storage-scalability-targets.md) numero hello di dischi non gestiti in un account di archiviazione** prima di aggiungere l'account di archiviazione di più dischi rigidi virtuali tooa
3. **Usare un account di archiviazione separato per ogni macchina virtuale di un set di disponibilità.** Non condividere account di archiviazione con più macchine virtuali in hello stesso Set di disponibilità. È accettabile per le macchine virtuali tra diversi account di archiviazione tooshare set di disponibilità se in precedenza le procedure consigliate sono seguite

## <a name="configure-each-application-tier-into-separate-availability-sets"></a>Configurare ogni livello dell'applicazione in set di disponibilità separati
Se le macchine virtuali sono tutti quasi identiche e vengono usati hello stesso scopo dell'applicazione, è consigliabile configurare un gruppo di disponibilità per ogni livello dell'applicazione.  Se si inseriscono due diversi livelli di in hello stesso set di disponibilità, tutte le macchine virtuali in hello stesso livello di applicazione può essere riavviato in una sola volta. Configurando almeno due macchine virtuali per ogni livello di un set di disponibilità, si garantisce la disponibilità di almeno una macchina virtuale in ogni livello.

Ad esempio, è possibile inserire tutte le macchine virtuali hello nel front-end di hello dell'applicazione in esecuzione IIS, Apache, Nginx in un unico set di disponibilità. Assicurarsi che solo le macchine virtuali front-end vengono posizionate in hello stesso set di disponibilità. e, analogamente, che in uno specifico set di disponibilità siano inserite solo le macchine virtuali livello dati, ad esempio le macchine virtuali di SQL Server replicate o MySQL.

<!--Image reference-->
   ![Livelli di applicazione](./media/virtual-machines-common-manage-availability/application-tiers.png)

## <a name="combine-a-load-balancer-with-availability-sets"></a>Combinare il bilanciamento del carico con set di disponibilità
Combinare hello [bilanciamento del carico di Azure](../articles/load-balancer/load-balancer-overview.md) con una disponibilità set hello tooget la maggior parte delle flessibilità di applicazione. Hello bilanciamento del carico di Azure distribuisce il traffico tra più macchine virtuali. Per le macchine virtuali il livello Standard, hello bilanciamento del carico di Azure è incluso. Non tutti i livelli di macchina virtuale includono hello bilanciamento del carico di Azure. Per altre informazioni sul bilanciamento del carico delle macchine virtuali, vedere [Load Balancing virtual machines](../articles/virtual-machines/virtual-machines-linux-load-balance.md) (Bilanciamento del carico delle macchine virtuali).

Se non è servizio di bilanciamento del carico hello configurato toobalance traffico tra più macchine virtuali, quindi qualsiasi evento di manutenzione pianificata interessa hello solo il traffico per macchina virtuale, causando un livello di applicazione tooyour di interruzione. Inserimento di più macchine virtuali di hello stesso livello in hello stesso bilanciamento del carico e disponibilità set consente il traffico toobe continuamente servito da almeno un'istanza.


<!-- Link references -->
[Configurare più macchine virtuali in un set di disponibilità per la ridondanza]: #configure-multiple-virtual-machines-in-an-availability-set-for-redundancy
[Configurare ogni livello dell'applicazione in set di disponibilità separati]: #configure-each-application-tier-into-separate-availability-sets
[Combinare il bilanciamento del carico con set di disponibilità]: #combine-a-load-balancer-with-availability-sets
[Avoid single instance virtual machines in availability sets]: #avoid-single-instance-virtual-machines-in-availability-sets
[Usare Managed Disks per le macchine virtuali nel set di disponibilità]: #use-managed-disks-for-vms-in-an-availability-set
