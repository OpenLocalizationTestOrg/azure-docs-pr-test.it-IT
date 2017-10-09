Macchine virtuali di Azure (VM) potrebbe talvolta il riavvio per alcun motivo apparente, senza la prova del che ha avviato dell'operazione di riavvio hello. Questo articolo vengono elencati hello azioni ed eventi che possono causare tooreboot macchine virtuali e forniscono informazioni dettagliate sulla modalità di tooavoid imprevisto riavviare problemi o ridurre l'impatto di hello di tali problemi.

## <a name="configure-hello-vms-for-high-availability"></a>Configurare le macchine virtuali hello per la disponibilità elevata
Riavvia Hello migliore modo tooprotect un'applicazione è in esecuzione in Azure da macchina virtuale e i tempi di inattività è tooconfigure hello, le macchine virtuali per la disponibilità elevata.

tooprovide questo livello di applicazione tooyour ridondanza, si consiglia di raggruppare due o più macchine virtuali in un set di disponibilità. Questa configurazione assicura che durante un evento di manutenzione pianificato o non pianificato, almeno una macchina virtuale sia disponibile e soddisfa al 99,95% di hello [SLA di Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_5/).

Per ulteriori informazioni sui set di disponibilità, vedere hello seguenti articoli:

- [Gestire la disponibilità di hello di macchine virtuali](../articles/virtual-machines/windows/manage-availability.md)
- [Configurare la disponibilità delle macchine virtuali](../articles/virtual-machines/windows/classic/configure-availability.md)

## <a name="resource-health-information"></a>Informazioni su Integrità risorse 
Integrità delle risorse di Azure è un servizio che espone integrità hello delle singole risorse di Azure e vengono fornite informazioni aggiuntive utilizzabili per la risoluzione dei problemi. In un ambiente cloud in cui non è possibile toodirectly server o accesso agli elementi dell'infrastruttura, obiettivo hello dell'integrità delle risorse è tooreduce hello tempo speso sulla risoluzione dei problemi. In particolare, l'obiettivo di hello è tooreduce hello tempi necessari per determinare se la radice hello del problema hello si trova in un'applicazione hello o in un evento all'interno di hello piattaforma Azure. Per altre informazioni, vedere [Panoramica su Integrità risorse di Azure](../articles/resource-health/resource-health-overview.md).

## <a name="actions-and-events-that-can-cause-hello-vm-tooreboot"></a>Azioni e gli eventi che possono causare hello tooreboot VM

### <a name="planned-maintenance"></a>Manutenzione pianificata
Microsoft Azure esegue periodicamente aggiornamenti tra hello globo tooimprove hello affidabilità, prestazioni e protezione dell'infrastruttura host hello sottostanti le macchine virtuali. Molti di questi aggiornamenti, inclusi gli aggiornamenti con mantenimento della memoria, vengono eseguiti senza alcun impatto sulle macchine virtuali o sui servizi cloud.

Altri aggiornamenti, invece, richiedono il riavvio. In questi casi, le macchine virtuali hello sono arrestate mentre è patch infrastruttura hello e riavviare le macchine virtuali hello.

toounderstand quali manutenzione pianificata di Azure e come può influenzare la disponibilità di hello delle macchine virtuali Linux, vedere gli articoli di hello elencati di seguito. articoli di Hello forniscono sfondo sul processo di manutenzione pianificata di Azure hello e come tooschedule pianificato manutenzione toofurther ridurre l'impatto di hello.

- [Manutenzione pianificata per le macchine virtuali in Azure](../articles/virtual-machines/windows/planned-maintenance.md)
- [Come tooschedule la manutenzione pianificata in macchine virtuali di Azure](../articles/virtual-machines/windows/classic/planned-maintenance-schedule.md)

### <a name="memory-preserving-updates"></a>Aggiornamenti con mantenimento della memoria   
Per questa classe di aggiornamenti in Microsoft Azure, gli utenti non notano alcun impatto sulle macchine virtuali in esecuzione. Molti di questi aggiornamenti sono toocomponents o servizi che possono essere aggiornati senza interferire con hello esegue l'istanza. Alcuni sono gli aggiornamenti dell'infrastruttura della piattaforma sul sistema operativo di host hello che possono essere applicate senza un riavvio di hello macchine virtuali.

Questi aggiornamenti con mantenimento della memoria vengono eseguiti con una tecnologia che consente la migrazione sul posto in tempo reale. Quando viene aggiornata, hello macchina virtuale si trova un *sospeso* stato. Questo stato mantiene memoria hello nella RAM mentre hello sistema operativo sottostante riceve le patch e aggiornamenti necessari hello. Hello VM viene ripreso entro 30 secondi di in pausa. Dopo aver hello che VM viene ripreso, l'orologio viene sincronizzato automaticamente.

A causa di periodo breve pausa hello, la distribuzione degli aggiornamenti tramite questo meccanismo notevolmente riduce l'impatto hello in hello macchine virtuali. Non si possono tuttavia distribuire tutti gli aggiornamenti in questo modo. 

Gli aggiornamenti a istanza multipla (per le macchine virtuali in un set di disponibilità) vengono applicati su un dominio di aggiornamento alla volta.

> [!NOTE]
> Con questo metodo di aggiornamento, i computer Linux con versioni precedenti del kernel sono interessati da un kernel panic. tooavoid questo problema, l'aggiornamento tookernel versione 3.10.0-327.10.1 o versione successiva. Per altre informazioni, vedere [Kernel panic di una macchina virtuale Linux di Azure basata su un kernel 3.10 dopo l'aggiornamento di nodo host](https://support.microsoft.com/help/3212236).     
    
### <a name="user-initiated-reboot-or-shutdown-actions"></a>Azioni di arresto o riavvio avviate dall'utente
 
Se si esegue il riavvio da hello portale di Azure, Azure PowerShell, interfaccia della riga di comando o reimpostare l'API, è possibile trovare l'evento hello in hello [Log attività Azure](../articles/monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

Se si esegue l'azione di hello dal sistema operativo della macchina virtuale di hello, è possibile trovare l'evento hello nei registri di sistema hello.

Altri scenari che in genere comportano hello VM tooreboot includono più azioni di modifica della configurazione. In genere verrà visualizzato un messaggio di avviso che indica che l'esecuzione di una determinata azione comporterà il riavvio di hello macchina virtuale. Esempi di operazioni di ridimensionamento qualsiasi macchina virtuale, modifica hello password dell'account amministrativo hello e l'impostazione di un indirizzo IP statico.

### <a name="azure-security-center-and-windows-update"></a>Centro sicurezza di Azure e Windows Update
Il Centro sicurezza di Azure monitora ogni giorno le macchine virtuali Windows e Linux alla ricerca di eventuali aggiornamenti mancanti del sistema operativo. Il Centro sicurezza recupera un elenco di aggiornamenti di sicurezza e critici disponibili da Windows Update o Windows Server Update Services (WSUS), in base al servizio configurato nella macchina virtuale Windows. Centro sicurezza PC controlla anche gli aggiornamenti più recenti di hello per i sistemi Linux. Se nella macchina virtuale non è stato eseguito un aggiornamento del sistema, il Centro sicurezza ne consiglia l'applicazione. un'applicazione Hello questi aggiornamenti del sistema viene controllata tramite hello Centro sicurezza PC in hello portale di Azure. Dopo l'applicazione di alcuni aggiornamenti, potrebbe essere necessario il riavvio della macchina virtuale. Per altre informazioni, vedere [Applicare gli aggiornamenti del sistema nel Centro sicurezza di Azure](../articles/security-center/security-center-apply-system-updates.md).

Analogamente a server locali, Azure non push degli aggiornamenti da Windows Update tooWindows macchine virtuali di Azure, poiché questi computer sono previsti toobe gestiti dagli utenti. Tuttavia sono incoraggiati tooleave hello impostazione automatica di Windows Update abilitato. Installazione automatica di aggiornamenti da Windows Update può causare toooccur riavvii dopo l'applicazione hello aggiornamenti. Per altre informazioni, vedere [Windows Update: domande frequenti](https://support.microsoft.com/help/12373/windows-update-faq).

### <a name="other-situations-affecting-hello-availability-of-your-vm"></a>Gli altri casi, compromettere hello disponibilità della macchina virtuale
Vi sono altri casi in cui Azure potrebbe attivamente sospendere utilizzare hello di una macchina virtuale. Si riceverà notifiche tramite posta elettronica prima di eseguire questa azione, per avere un tooresolve possibilità hello problemi sottostanti. Violazioni della sicurezza e la scadenza di hello di metodi di pagamento sono esempi di problemi che influiscono sulla disponibilità delle macchine Virtuali.

### <a name="host-server-faults"></a>Errori del server host 
Hello macchina virtuale è ospitato in un server fisico in cui è in esecuzione all'interno di un Data Center Azure. Hello server fisico in esecuzione un agente denominato Ciao agente Host tooa inoltre alcuni altri componenti di Azure. Quando questi componenti software di Azure nel server fisico hello rispondono, sistema di monitoraggio hello attiva un riavvio hello host tooattempt di ripristino del server. Hello macchina virtuale è in genere disponibile entro cinque minuti e continua toolive su hello stesso host in precedenza.

Errori server sono in genere causati da un errore hardware, ad esempio un errore di un disco rigido o un'unità SSD hello. Azure continuamente monitora le occorrenze, identifica i bug di hello sottostante e rilascia gli aggiornamenti dopo l'attenuazione hello impostate e testate.

Poiché alcuni errori del server host possono essere server toothat specifico, una situazione di riavvio VM ripetuta potrebbe essere migliorata effettuando manualmente un server host macchina virtuale tooanother hello. Questa operazione può essere attivata utilizzando hello **ridistribuire** opzione nella pagina dettagli hello di hello VM, o arrestando e riavviando hello VM nel portale di Azure hello.

### <a name="auto-recovery"></a>Ripristino automatico
Se per qualsiasi motivo non è possibile riavviare i server host hello, hello piattaforma Azure avvia un server host non corretto hello di recupero automatico azione tootake dalla rotazione per un'analisi più approfondita. 

Tutte le macchine virtuali nell'host sono server host diverso, integro tooa riposizionato automaticamente. Questo processo richiede in genere 15 minuti. toolearn più sul processo di ripristino automatico di hello, vedere [recupero automatico delle macchine virtuali](https://azure.microsoft.com/blog/service-healing-auto-recovery-of-virtual-machines).

### <a name="unplanned-maintenance"></a>Manutenzione non pianificata
In rari casi, salve team di operazioni di Azure potrebbe essere necessario tooensure le attività di manutenzione tooperform hello integrità complessiva di hello piattaforma Azure. Questo comportamento potrebbe influire sulla disponibilità VM e determina in genere hello stessa azione di recupero automatico, come descritto in precedenza.  

Non pianificato maintenances includere hello informazioni seguenti:

- Deframmentazione urgente di un nodo
- Aggiornamenti urgenti di switch di rete

### <a name="vm-crashes"></a>Arresti anomali della macchina virtuale
Macchine virtuali potrebbe essere riavviato a causa di problemi all'interno di hello macchina virtuale stessa. carico di lavoro Hello o un ruolo in esecuzione su hello VM potrebbe attivare un controllo bug all'interno del sistema operativo guest di hello. Per determinare il motivo di hello di arresto anomalo di hello, visualizzare i registri di sistema e dell'applicazione hello per le macchine virtuali Windows e hello registri seriali per le macchine virtuali Linux.

### <a name="storage-related-forced-shutdowns"></a>Arresti forzati correlati all'archiviazione
Macchine virtuali in Azure si basano su dischi virtuali per sistema operativo e l'archiviazione di dati che è ospitato nell'infrastruttura di archiviazione di Azure hello. Ogni volta che la disponibilità di hello o la connettività tra hello macchine Virtuali e dischi virtuali associato hello è interessata da più di 120 secondi, hello piattaforma Azure esegue un arresto forzato di un danneggiamento dei dati di macchine virtuali tooavoid hello. macchine virtuali Hello vengono automaticamente attivate nuovamente dopo il ripristino di connettività dell'archiviazione. 

durata Hello dell'arresto hello può essere più breve cinque minuti, ma può essere notevolmente più lunga. di seguito Hello è uno dei casi specifici hello associata con l'arresto forzato all'archiviazione: 

**Superamento dei limiti di I/O**

Macchine virtuali potrebbero essere temporaneamente interrotto quando le richieste dei / o sono limitate in modo coerente perché il volume di hello di operazioni dei / o al secondo (IOPS) supera i limiti di hello i/o disco hello. (Spazio su disco standard è limitato IOPS too500.) toomitigate questo problema, utilizzare lo striping del disco o configurare spazi di archiviazione hello all'interno di hello guest macchina virtuale, a seconda del carico di lavoro di hello. Per altre informazioni, vedere [Configurazione delle macchine virtuali di Azure per prestazioni di archiviazione ottimali](http://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx).

Limiti più elevati di IOPS sono disponibili tramite l'archiviazione Premium di Azure con backup too80, IOPS 000. Per altre informazioni, vedere [Archiviazione Premium con prestazioni elevate](../articles/storage/common/storage-premium-storage.md).

### <a name="other-incidents"></a>Altri eventi imprevisti
In rare circostanze, un problema di ampia portata può interessare più server in un data center di Azure. Se si verifica questo problema, hello team Azure Invia messaggio di posta elettronica le sottoscrizioni di notifiche toohello interessata. È possibile controllare hello [dashboard di integrità del servizio Azure](https://azure.microsoft.com/status/) e hello portale di Azure per lo stato di hello delle interruzioni in corso e dopo gli eventi imprevisti.
