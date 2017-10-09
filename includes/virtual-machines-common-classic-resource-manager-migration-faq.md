# <a name="frequently-asked-questions-about-classic-tooazure-resource-manager-migration"></a>Domande frequenti sulla migrazione di gestione risorse di tooAzure classico

## <a name="does-this-migration-plan-affect-any-of-my-existing-services-or-applications-that-run-on-azure-virtual-machines"></a>Il piano di migrazione influisce sui servizi o sulle applicazioni esistenti in esecuzione nelle macchine virtuali di Azure? 

No. Hello macchine virtuali (classiche) sono completamente supportati i servizi in disponibilità generale. È possibile continuare a toouse tooexpand queste risorse footprint in Microsoft Azure.

## <a name="what-happens-toomy-vms-if-i-dont-plan-on-migrating-in-hello-near-future"></a>Macchine virtuali toomy cosa accade se non prevede la migrazione di hello prossimo futuro? 

Non ci stiamo deprecazione hello classic API e risorse modello esistente. Vogliamo toomake migrazione semplice, prendendo in considerazione le funzionalità disponibili nel modello di distribuzione di gestione risorse di hello avanzate hello. Si consiglia di rivedere [alcuni dei miglioramenti hello](../articles/azure-resource-manager/resource-manager-deployment-model.md) che fanno parte di IaaS in Gestione risorse.

## <a name="what-does-this-migration-plan-mean-for-my-existing-tooling"></a>Qual è l'impatto di questo piano di migrazione per gli strumenti esistenti? 

L'aggiornamento del modello di distribuzione gli strumenti di gestione delle risorse toohello è una delle modifiche più importanti hello che è necessario tooaccount nei piani di migrazione.

## <a name="how-long-will-hello-management-plane-downtime-be"></a>Quanto tempo i tempi di inattività di hello gestione piano sarà? 

Dipende dal numero di hello delle risorse migrate. Per le distribuzioni di dimensioni minori (poche decine di macchine virtuali), hello intera migrazione deve richiedere da meno di un'ora. Per le distribuzioni su larga scala (centinaia di macchine virtuali), migrazione di hello può richiedere alcune ore.

## <a name="can-i-roll-back-after-my-migrating-resources-are-committed-in-resource-manager"></a>È possibile eseguire il rollback dopo il commit delle risorse sottoposte a migrazione in Resource Manager? 

È possibile interrompere la migrazione, purché le risorse di hello sono in stato preparato hello. Eseguire il rollback non è supportato dopo risorse hello sono state migrate correttamente tramite l'operazione di commit hello.

## <a name="can-i-roll-back-my-migration-if-hello-commit-operation-fails"></a>È possibile ripristinare la migrazione se si verifica un errore di operazione di commit hello? 

Se l'operazione di commit hello ha esito negativo, non è possibile terminare la migrazione. Tutte le operazioni di migrazione, inclusi l'operazione di commit hello sono idempotenti. Pertanto, è consigliabile che ripetere l'operazione di hello dopo un breve periodo di tempo. Se si resta un errore, creare un ticket di supporto o creare un post del forum con tag ClassicIaaSMigration hello nostri [forum VM](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).

## <a name="do-i-have-toobuy-another-express-route-circuit-if-i-have-toouse-iaas-under-resource-manager"></a>È necessario toobuy un altro circuito express route se si hanno toouse IaaS in Gestione risorse? 

No. È abilitato il recente [lo spostamento di circuiti ExpressRoute dal modello di distribuzione di gestione risorse toohello classico hello](../articles/expressroute/expressroute-move.md). Non è necessario toobuy un nuovo circuito ExpressRoute se hai già uno.

## <a name="what-if-i-had-configured-role-based-access-control-policies-for-my-classic-iaas-resources"></a>Che cosa succede se sono stati configurati criteri di controllo degli accessi in base al ruolo per le risorse IaaS classiche? 

Durante la migrazione, le risorse di hello trasformare dalla classica tooResource Manager. Pertanto, è consigliabile pianificare gli aggiornamenti di criteri RBAC hello necessarie toohappen dopo la migrazione.

## <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>È stato eseguito il backup di VM della versione classica in un insieme di credenziali di backup. È possibile eseguire la migrazione di macchine virtuali dalla modalità di gestione in modalità classica tooResource e la protezione in un insieme di credenziali di servizi di ripristino? 

Classico i punti di ripristino di macchine Virtuali in un insieme di credenziali di backup non vengono migrati insieme di credenziali di servizi di ripristino tooa automaticamente quando si sposta hello VM da tooResource classico in modalità di gestione. Seguire questi passaggi tootransfer i backup VM:

1. Nell'insieme di credenziali Backup hello passare toohello **elementi protetti** e selezionare hello macchina virtuale. Fare clic su [Arresta protezione](../articles/backup/backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Lasciare *deselezionata* l'opzione **Elimina i dati di backup associati**.
2. Eliminare l'estensione di snapshot di backup/hello dalla hello macchina virtuale.
3. Eseguire la migrazione di macchine virtuali hello dalla modalità di gestione tooResource modalità classica. Verificare che le informazioni di archiviazione e rete hello macchina virtuale toohello corrispondente viene anche eseguita la migrazione tooResource modalità di gestione.
4. Creare un insieme di credenziali di servizi di ripristino e configurare i backup su hello migrazione macchina virtuale utilizzando **Backup** azione nella parte superiore del dashboard dell'insieme di credenziali. Per informazioni dettagliate sul backup dei servizi di ripristino tooa macchina virtuale insieme di credenziali, vedere l'articolo di hello, [proteggere macchine virtuali di Azure con un insieme di credenziali di servizi di ripristino](../articles/backup/backup-azure-vms-first-look-arm.md).

## <a name="can-i-validate-my-subscription-or-resources-toosee-if-theyre-capable-of-migration"></a>È possibile convalidare la sottoscrizione o risorse toosee se sono in grado di migrazione? 

Sì. Nell'opzione di migrazione supportata dalla piattaforma hello, innanzitutto hello in preparazione per la migrazione è toovalidate che le risorse di hello siano in grado di migrazione. Nel caso in cui hello convalidare l'operazione ha esito negativo, si ricevono messaggi per i motivi hello non è possibile completare la migrazione di hello.

## <a name="what-happens-if-i-run-into-a-quota-error-while-preparing-hello-iaas-resources-for-migration"></a>Cosa succede se si esegue un errore di quota durante la preparazione per la migrazione di risorse IaaS hello? 

Si consiglia di interrompere la migrazione e quindi accedere le quote di hello un supporto richiesta tooincrease hello area geografica in cui eseguire la migrazione hello macchine virtuali. Dopo l'approvazione richiesta di quota hello, è possibile iniziare a eseguire di nuovo i passaggi della migrazione hello.

## <a name="how-do-i-report-an-issue"></a>Come si segnala un problema? 

Registrare i problemi e domande sulla migrazione tooour [forum VM](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows), con la parola chiave hello ClassicIaaSMigration. Si consiglia di pubblicare tutte le eventuali domande in questo forum. Se si dispone di un contratto di assistenza, si è benvenuto toolog anche un ticket di supporto.

## <a name="what-if-i-dont-like-hello-names-of-hello-resources-that-hello-platform-chose-during-migration"></a>Cosa accade se non è soddisfacente nomi hello risorse hello hello piattaforma scelto durante la migrazione? 

Tutte le risorse hello è fornire in modo esplicito i nomi di modello di distribuzione classica hello vengono mantenute durante la migrazione. In alcuni casi vengono create nuove risorse. Ad esempio, viene creata un'interfaccia di rete per ogni VM. Hello possibilità toocontrol hello nomi di queste nuove risorse creati durante la migrazione non è attualmente supportato. Registrare i voti per questa funzionalità in hello [forum sul feedback Azure su](http://feedback.azure.com).

## <a name="can-i-migrate-expressroute-circuits-used-across-subscriptions-with-authorization-links"></a>È possibile eseguire la migrazione dei circuiti ExpressRoute usati in diverse sottoscrizioni con i collegamenti di autorizzazione? 

Non è possibile eseguire automaticamente la migrazione dei circuiti ExpressRoute che usano collegamenti di autorizzazione tra sottoscrizioni senza tempi di inattività. Sono disponibili indicazioni su come eseguire la questa migrazione seguendo una procedura manuale. Vedere [ExpressRoute di eseguire la migrazione di circuiti e associate reti virtuali dal modello di distribuzione di gestione risorse toohello classico hello](../articles/expressroute/expressroute-migration-classic-resource-manager.md) per passaggi e altre informazioni.

## <a name="i-got-a-message-vm-is-reporting-hello-overall-agent-status-as-not-ready-hence-hello-vm-cannot-be-migrated-ensure-that-hello-vm-agent-is-reporting-overall-agent-status-as-ready-or-vm-contains-extension-whose-status-is-not-being-reported-from-hello-vm-hence-this-vm-cannot-be-migrated-"></a>Viene visualizzato un messaggio *"macchina virtuale è reporting hello complessiva dello stato agente come non pronto. Di conseguenza, non può essere migrato hello macchina virtuale. Verificare che l'agente VM hello è reporting stato agente generale come pronto per la"* o *"macchina virtuale contiene il cui stato non viene segnalato da hello macchina virtuale di estensione. Per questo motivo, non è possibile eseguire la migrazione della macchina virtuale". *

Questo messaggio viene ricevuto quando hello macchina virtuale non dispone di connettività in uscita toohello internet. agente VM Hello Usa account di archiviazione di Azure hello tooreach connettività in uscita per l'aggiornamento di stato dell'agente hello ogni cinque minuti.
