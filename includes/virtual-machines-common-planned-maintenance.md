Azure esegue periodicamente aggiornamenti tooimprove hello affidabilità, prestazioni e protezione dell'infrastruttura host hello per le macchine virtuali. Questi aggiornamenti compresi tra l'applicazione di patch i componenti software hello hosting ambiente (ad esempio sistema operativo, hypervisor e vari agenti siano distribuiti in host hello), l'aggiornamento di componenti di rete, toohardware rimozione delle autorizzazioni. la maggior parte Hello di questi aggiornamenti vengono eseguite senza tutte le macchine virtuali ospitata toohello impatto. Ci sono casi tuttavia in cui gli aggiornamenti hanno conseguenze:

- Se la manutenzione hello non richiede un riavvio, Azure Usa hello toopause migrazione sul posto VM mentre host hello viene aggiornato.

- Se manutenzione richiede un riavvio, viene visualizzato un avviso quando viene pianificata manutenzione hello. In questi casi, verranno anche presentate un intervallo di tempo in cui è possibile avviare manutenzione hello manualmente, in un momento appropriato.

Questa pagina descrive come Microsoft Azure esegue entrambi i tipi di manutenzione. Per ulteriori informazioni sugli eventi non pianificati (interruzioni), vedere disponibilità hello di gestione delle macchine virtuali per [Windows] (... / articles/virtual-machines/windows/manage-availability.md) o [Linux](../articles/virtual-machines/linux/manage-availability.md).

Hello di applicazioni in esecuzione in una macchina virtuale possono raccogliere informazioni sugli aggiornamenti futuri utilizzando i metadati di servizio per [Windows](../articles/virtual-machines/windows/instance-metadata-service.md) o [Linux] (... / articles/virtual-machines/linux/instance-metadata-service.md).

## <a name="in-place-vm-migration"></a>Migrazione di una VM sul posto

Quando gli aggiornamenti non richiedono un riavvio completo, viene usata una migrazione in tempo reale sul posto. Durante l'aggiornamento di hello macchina virtuale hello viene sospesa per circa 30 secondi, mantenendo la memoria hello nella RAM, mentre hello ambiente di hosting si applica patch e aggiornamenti necessari hello. macchina virtuale Hello viene quindi ripreso e il clock di hello della macchina virtuale hello viene sincronizzato automaticamente.

Per le VM nei set di disponibilità, i domini di aggiornamento vengono aggiornati uno alla volta. Tutte le macchine virtuali in un dominio di aggiornamento (UD) in pausa, aggiornamento e quindi riavviate prima che la manutenzione pianificata Sposta toohello UD successivo.

Alcune applicazioni potrebbero essere interessate da questi tipi di aggiornamenti. Applicazioni che eseguono in tempo reale elaborazione di eventi, come i flussi multimediali o transcodifica o ad alta velocità effettiva di rete scenari, potrebbero non essere tootolerate progettato una pausa secondo 30. <!-- sooooo, what should they do? --> 


## <a name="maintenance-requiring-a-reboot"></a>Manutenzione per cui è necessario un riavvio

Quando le macchine virtuali devono toobe riavviato per la manutenzione pianificata, ricevono una notifica in anticipo. Manutenzione pianificata ha due fasi: hello finestra self-service e una finestra di manutenzione pianificata.

Hello **self-service finestra** consente di avviare la manutenzione hello le macchine virtuali. Durante questo periodo, è possibile richiedere toosee ogni VM il relativo stato e verificare il risultato di hello dell'ultima richiesta di manutenzione.

Quando si avvia manutenzione self-service, la macchina virtuale è spostato tooa nodo che è già stato aggiornato e quindi viene acceso viene nuovamente. Poiché il riavvio di hello macchina virtuale, disco temporaneo hello viene perso e vengono aggiornati gli indirizzi IP dinamici associati con l'interfaccia di rete virtuale.

Se si avvia manutenzione self-service e si verifica un errore durante il processo di hello, hello operazione viene arrestata, hello VM non viene aggiornata e viene rimossa anche da hello pianificato manutenzione iterazione. Si verrà contattati in un secondo momento con una nuova pianificazione e offerto una nuova opportunità toodo self-service la manutenzione. 

Quando viene superato finestra self-service di hello, hello **finestra di manutenzione pianificata** inizia. Durante questo intervallo di tempo, è possibile comunque una query per la finestra di manutenzione hello, ma non è più possibile toostart in grado di manutenzione di hello.

## <a name="availability-considerations-during-planned-maintenance"></a>Considerazioni sulla disponibilità durante la manutenzione pianificata 

Se si decide di toowait fino a quando non hello pianificata la finestra di manutenzione, esistono alcuni aspetti tooconsider per la gestione di hello disponibilità più elevata delle macchine virtuali. 

### <a name="paired-regions"></a>Aree associate

Ogni area di Azure è associato a un'altra area all'interno di hello stesso geografia, insieme rendono una coppia internazionale. Durante la manutenzione pianificata, Azure aggiornerà solo le macchine virtuali in una singola area di una coppia di area hello. Ad esempio, quando si aggiorna hello macchine virtuali in North Central US, Azure non aggiornerà tutte le macchine virtuali nel centro-meridionali in hello contemporaneamente. Tuttavia, le altre aree, ad esempio Europa settentrionale può essere in fase di manutenzione in hello stesso tempo come Stati Uniti orientali. Sapendo come funzionano le coppie di aree, è possibile distribuire meglio le VM tra le aree. Per altre informazioni, vedere [Coppie di aree di Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="availability-sets-and-scale-sets"></a>Set di disponibilità e set di disponibilità

Quando si distribuisce un carico di lavoro nelle macchine virtuali di Azure, è possibile creare macchine virtuali di hello all'interno di un'applicazione di tooyour disponibilità set tooprovide la disponibilità elevata. Ciò assicura che in caso di interruzione o di eventi di manutenzione sia disponibile almeno una macchina virtuale.

All'interno di un set di disponibilità, singole macchine virtuali vengono distribuite tra i domini di aggiornamento too20 (UD). Durante la manutenzione pianificata, l'impatto prodotto interessa un solo dominio di aggiornamento in un dato momento Tenere presente che ordine hello di domini di aggiornamento influenzate non necessariamente avvengono in modo sequenziale. 

Set di scalabilità di macchine virtuali sono una risorsa di calcolo di Azure che consente di toodeploy e gestire un set di macchine virtuali identiche come una singola risorsa. set di scalabilità Hello viene distribuito automaticamente nei domini di aggiornamento, ad esempio macchine virtuali in un set di disponibilità. Esattamente come con i set di disponibilità, con i set di scalabilità viene interessato un solo dominio di aggiornamento per volta.

Per ulteriori informazioni sulla configurazione delle macchine virtuali per la disponibilità elevata, vedere la disponibilità di hello di gestione delle macchine virtuali per Windows (... / articles/virtual-machines/windows/manage-availability.md) o [Linux](../articles/virtual-machines/linux/manage-availability.md).
