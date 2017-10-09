


Questo articolo illustra alcune domande comuni che gli utenti di richiedere sulle macchine virtuali di Azure create con il modello di distribuzione classica hello.

## <a name="can-i-migrate-my-vm-created-in-hello-classic-deployment-model-toohello-new-resource-manager-model"></a>È possibile eseguire la migrazione la macchina virtuale creata in hello classico modello toohello nuovo gestore di risorse modello di distribuzione?
Sì. Per istruzioni su come toomigrate, vedere:

* [Eseguire la migrazione da tooAzure classico gestore delle risorse con Azure PowerShell](../articles/virtual-machines/windows/migration-classic-resource-manager-ps.md).
* [Eseguire la migrazione da tooAzure classico Gestione risorse mediante Azure CLI](../articles/virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md).

## <a name="what-can-i-run-on-an-azure-vm"></a>Cosa è possibile eseguire in una VM di Azure?
Tutti i sottoscrittori possono eseguire software del server in una macchina virtuale Azure. È possibile eseguire versioni recenti di Windows Server, nonché un'ampia gamma di distribuzioni di Linux. Per ulteriori informazioni di supporto, vedere:

• Per VM di Windows - [Supporto del software del server Microsoft per macchine virtuali di Azure](http://go.microsoft.com/fwlink/p/?LinkId=393550)

• Per VM di Linux -- [Distribuzioni di Linux supportate da Azure](http://go.microsoft.com/fwlink/p/?LinkId=393551)

Per le immagini client Windows, alcune versioni di Windows 7 e Windows 8.1 sono disponibili tooMSDN Azure sottoscrittori di benefit e i sottoscrittori MSDN sviluppo e Test pagamento a consumo, per le attività di sviluppo e test. Per ulteriori informazioni, incluse le istruzioni e limitazioni, vedere [Immagini Client Windows per gli abbonati MSDN](https://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/).

## <a name="why-are-affinity-groups-being-deprecated"></a>Perché i gruppi di affinità sono deprecati?
I gruppi di affinità sono un concetto legacy per un raggruppamento geografico delle distribuzioni di servizi cloud di un cliente e degli account di archiviazione in Azure. Sono stati forniti originariamente tooimprove prestazioni della rete VM per VM in progettazioni di rete di Azure anticipata hello. Sono inoltre supportati versione iniziale di hello di reti virtuali (Vnet), che sono stati tooa limitato piccolo set di componenti hardware in un'area.

rete Azure Hello corrente all'interno di un'area è progettato in modo che i gruppi di affinità non sono più necessari. Le reti virtuali fanno anche parte di un ambito a livello di area, quindi un gruppo di affinità non è più necessario quando si usa una rete virtuale. A causa di miglioramenti toothese, non è più consigliabile ai clienti di utilizzare gruppi di affinità perché può essere limitazione in alcuni scenari. Utilizzo dei gruppi di affinità inutilmente assocerà l'hardware toospecific macchine virtuali che limita la scelta di hello di dimensioni delle macchine Virtuali che sono disponibili tooyou. Quando si tenta di tooadd nuove macchine virtuali se l'hardware specifico hello associata al gruppo di affinità hello è vicino a capacità, è possibile che gli errori relativi a toocapacity.

La funzionalità gruppo di affinità già è deprecata nel modello di distribuzione Azure Resource Manager hello in hello portale di Azure. Per il portale di Azure classico di hello, ci stiamo deprecazione di supporto per la creazione di gruppi di affinità e la creazione di risorse di archiviazione che appartengono al gruppo di affinità tooan bloccati. Non è necessario toomodify i servizi cloud esistenti che utilizzano un gruppo di affinità. I nuovi servizi cloud non dovranno invece usare gruppi di affinità, a meno che questo approccio non sia consigliato da un tecnico di Azure.

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Quanta memoria è possibile utilizzare con una macchina virtuale?
Ogni disco dati può essere backup too1 TB. numero di Hello di dischi di dati che è possibile utilizzare dipende dalle dimensioni hello della macchina virtuale hello. Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Un account di archiviazione di Azure fornisce archiviazione per disco del sistema operativo hello e per eventuali dischi dati. Ogni disco è un file con estensione vhd archiviato come BLOB di pagine. Per informazioni sui prezzi, vedere [Dettagli prezzi di archiviazione](http://go.microsoft.com/fwlink/p/?LinkId=396819).

## <a name="which-virtual-hard-disk-types-can-i-use"></a>Quali tipi di disco rigido virtuale è possibile utilizzare?
Azure supporta solo dischi rigidi virtuali fissi in formato VHD. Se si dispone di un file VHDX che si desidera toouse in Azure, è necessario toofirst convertirlo mediante la gestione di Hyper-V o hello [convert-VHD](http://go.microsoft.com/fwlink/p/?LinkId=393656) cmdlet. Una volta a tale scopo, utilizzare [Add-AzureVHD](https://msdn.microsoft.com/library/azure/dn495173.aspx) hello tooupload cmdlet (in modalità di gestione del servizio) account di archiviazione tooa VHD in Azure è possibile utilizzarlo con le macchine virtuali.

* Per istruzioni di Linux, vedere [creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux di hello](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
* Per istruzioni di Windows, vedere [creazione e caricamento di un disco rigido virtuale di Windows Server di tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="are-these-virtual-machines-hello-same-as-hyper-v-virtual-machines"></a>Coincidono che Hello queste macchine virtuali come macchine virtuali Hyper-V?
In molti modi in cui si simile troppo le macchine virtuali Hyper-V "Generazione 1", ma è non esattamente hello stesso. Entrambi i tipi forniscono hardware virtualizzato e dischi rigidi virtuali di hello formato VHD sono compatibili. Ciò significa che è possibile spostarli tra Hyper-V e Azure. Tre differenze principali che talvolta sorprendono gli utenti di Hyper-V sono:

* Azure non fornisce una macchina virtuale di tooa accesso console. Non vi è alcun tooaccess modo una macchina virtuale fino al termine l'avvio.
* Le macchine virtuali di Azure nella maggior parte delle [dimensioni](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) dispongono di una sola scheda di rete virtuale, pertanto possono avere un solo indirizzo IP esterno. (hello A8 e A9 dimensioni usano una seconda scheda di rete per la comunicazione delle applicazioni tra le istanze in scenari limitati.)
* Le macchine virtuali di Azure non supportano le funzionalità della macchina virtuale Hyper-V di seconda generazione. Per informazioni dettagliate su queste funzionalità, vedere [Specifiche delle macchine virtuali per Hyper-V](http://technet.microsoft.com/library/dn592184.aspx) e [Panoramica delle macchine virtuali di seconda generazione](https://technet.microsoft.com/library/dn282285.aspx).

## <a name="can-these-virtual-machines-use-my-existing-on-premises-networking-infrastructure"></a>Queste macchine virtuali possono utilizzare l’infrastruttura di rete locale esistente?
Per le macchine virtuali create nel modello di distribuzione classica hello, è possibile utilizzare l'infrastruttura esistente tooextend di rete virtuale di Azure. approccio Hello corrisponde all'impostazione di una succursale. È possibile eseguire il provisioning e gestire reti private virtuali (VPN) in Azure, nonché collegarle in modo sicuro tooon locale infrastruttura IT. Per informazioni dettagliate, vedere [Panoramica della rete virtuale](../articles/virtual-network/virtual-networks-overview.md).

È necessario rete hello toospecify che si desidera hello toowhen toobelong macchina virtuale si crea una macchina virtuale hello. È possibile collegare una rete virtuale tooa macchina virtuale esistente. Tuttavia, è possibile risolvere il problema, scollegare hello disco virtuale (VHD) dalla macchina virtuale esistente hello e quindi utilizzarlo toocreate una nuova macchina virtuale con la configurazione di rete hello desiderato.

## <a name="how-can-i-access--my-virtual-machine"></a>Come si accede alla macchina virtuale?
È necessario tooestablish toolog una connessione remota nella macchina virtuale toohello tramite connessione Desktop remoto per una macchina virtuale Windows o un Secure Shell (SSH) per una VM Linux. Per le istruzioni, vedere

* [Come tooLog nella macchina virtuale che esegue Windows Server tooa](../articles/virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Sono supportati un massimo di connessioni simultanee 2, a meno che non hello server è configurato come un host di sessione di Servizi Desktop remoto.  
* [Come tooLog nella macchina virtuale che esegue Linux tooa](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Per impostazione predefinita, la SSH consente un massimo di 10 connessioni simultanee. È possibile aumentare questo numero modificando il file di configurazione di hello.

Se si verificano problemi con Desktop remoto o SSH, installare e utilizzare hello [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) estensione toohelp risolto hello problema.

Per le macchine virtuali Windows, opzioni aggiuntive includono:

* In hello portale di Azure classico, trovare hello macchina virtuale, quindi fare clic su **Reimposta accesso remoto** hello barra dei comandi.
* Revisione [tooa connessioni Desktop remoto di risoluzione dei problemi basato su Windows Azure Virtual Machine](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Utilizzare Windows PowerShell Remoting tooconnect toohello VM o creare endpoint aggiuntivi per altri toohello tooconnect risorse macchina virtuale. Per informazioni dettagliate, vedere [come configurare gli endpoint di tooSet tooa macchina virtuale](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Se si ha familiarità con Hyper-V, si potrebbe cercando un tooVMConnect simile dello strumento. Azure non offre uno strumento simile perché macchina virtuale di tooa accesso console non è supportato.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-for-windows-or-devsdb1-for-linux-toostore-data"></a>È possibile utilizzare i dati di toostore hello disco temporaneo (Buongiorno unità d: per Windows o /dev/sdb1 per Linux)?
È consigliabile utilizzare i dati di toostore hello disco temporaneo (Buongiorno unità d: per impostazione predefinita per Windows o /dev/sdb1 per Linux). Si tratta solo di memorie temporanee, pertanto si rischierebbe di perdere dati che non possono essere recuperati. Ciò può verificarsi quando macchina virtuale hello Sposta tooa un host diverso. Ridimensionamento di una macchina virtuale, l'aggiornamento host hello o un errore hardware nell'host di hello è riportati alcuni dei motivi hello che potrebbe spostare una macchina virtuale.

## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Come è possibile modificare la lettera di unità hello del disco temporaneo hello?
In una macchina virtuale di Windows, è possibile modificare la lettera di unità hello per lo spostamento del file pagina hello e riassegnando le lettere di unità, ma è necessario toomake che si hello passaggi in un ordine specifico. Per istruzioni, vedere [lettera di unità di modifica hello del disco temporaneo di Windows hello](../articles/virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="how-can-i-upgrade-hello-guest-operating-system"></a>Come è possibile l'aggiornamento del sistema operativo guest di hello?
Hello termine aggiornamento indica in genere tooa mobile più recente versione del sistema operativo, mantenendo hello stesso hardware. Per le macchine virtuali di Azure, hello processo per lo spostamento tooa versione più recente è diverso per Linux e Windows:

* Per le macchine virtuali Linux, usare strumenti di gestione dei pacchetti hello e le procedure appropriate per la distribuzione di hello.
* Per una macchina virtuale di Windows, è necessario il server di hello toomigrate utilizzando simile hello strumenti di migrazione per Windows Server. Non tentare di sistema operativo guest di hello tooupgrade mentre risiede in Azure. Non è supportato a causa del rischio di hello di perdita di macchina virtuale toohello di accesso. Se si verificano problemi durante l'aggiornamento di hello, si potrebbe perdere hello possibilità toostart un Desktop remoto della sessione e non sarebbe in grado di tootroubleshoot problemi hello.

Per informazioni generali sugli strumenti hello e i processi per la migrazione di un Server Windows, vedere [tooWindows di eseguire la migrazione di ruoli e funzionalità Server](http://go.microsoft.com/fwlink/p/?LinkId=396940).

## <a name="whats-hello-default-user-name-and-password-on-hello-virtual-machine"></a>Che cos'è il nome utente predefiniti hello e la password nella macchina virtuale hello?
immagini Hello fornite da Azure non sono un nome utente configurati in precedenza e una password. Quando si crea una macchina virtuale utilizzando una di queste immagini, è necessario tooprovide un nome utente e password, si userà toolog sulla macchina virtuale toohello.

Se hai dimenticato la password o nome utente hello ed è stato installato l'agente VM hello, è possibile installare e utilizzare hello [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) problema hello toofix di estensione.

Informazioni aggiuntive:

* Per le immagini Linux hello, se si utilizza hello portale di Azure classico, 'azureuser' è specificato come un nome utente predefinito, ma è possibile modificare questa impostazione utilizzando 'Da raccolta' anziché 'Creazione rapida' come macchina virtuale di hello modo toocreate hello. Utilizzando 'Da raccolta' consente inoltre di decidere se toouse una password, una chiave SSH o entrambe toolog in. account utente Hello è un utente senza privilegi che dispone di accesso 'sudo' toorun comandi con privilegi. account 'root' Hello è disabilitato.
* Per le immagini di Windows, è necessario tooprovide un nome utente e password quando si crea hello macchina virtuale. account di Hello viene aggiunto il gruppo di amministratori toohello.

## <a name="can-azure-run-anti-virus-on-my-virtual-machines"></a>Azure è in grado di eseguire software antivirus nelle macchine virtuali?
Azure offre diverse opzioni per le soluzioni antivirus, ma è attivo tooyou toomanage è. Ad esempio, potrebbe essere una sottoscrizione separata per il software antimalware, e sarà necessario toodecide quando toorun esegue l'analisi e installare gli aggiornamenti. È possibile aggiungere il supporto antivirus con un'estensione VM per Microsoft Antimalware, Symantec Endpoint Protection o TrendMicro Deep Security Agent quando si crea una macchina virtuale Windows o in un momento successivo. Hello Symantec e TrendMicro estensioni consentono di utilizzare una sottoscrizione di valutazione gratuita di tempo limitato o una sottoscrizione aziendale esistente. Microsoft Antimalware è disponibile gratuitamente. Per informazioni dettagliate, vedere:

* [Come tooinstall e configurare Symantec Endpoint Protection in una macchina virtuale di Azure](http://go.microsoft.com/fwlink/p/?LinkId=404207)
* [Come tooinstall e configurare Trend Micro Deep Security come servizio in una macchina virtuale di Azure](http://go.microsoft.com/fwlink/p/?LinkId=404206)
* [Distribuzione di soluzioni antimalware in macchine virtuali di Azure](https://azure.microsoft.com/blog/2014/05/13/deploying-antimalware-solutions-on-azure-virtual-machines/)

## <a name="what-are-my-options-for-backup-and-recovery"></a>Quali sono le opzioni per il backup e il ripristino?
Backup di Azure è disponibile come anteprima in alcune aree. Per informazioni dettagliate, vedere [Backup delle macchine virtuali di Azure](../articles/backup/backup-azure-vms.md). Altre soluzioni sono disponibili da partner certificati. toofind sulle risorse attualmente disponibili, eseguire la ricerca hello Azure Marketplace.

Un'altra opzione è una funzionalità di snapshot hello toouse dell'archiviazione blob. toodo, sarà necessario tooshut verso il basso hello VM prima di qualsiasi operazione che si basa su uno snapshot del blob. Questo consente di salvare i dati in sospeso scritture e inserisce sistema file hello in uno stato coerente.

## <a name="how-does-azure-charge-for-my-vm"></a>Come viene addebitata la VM da Azure?
Azure addebita un costo orario in base alle dimensioni della macchina virtuale di hello e del sistema operativo. Per le ore parziali, Azure addebita solo per i minuti di hello di utilizzo. Se si crea hello macchina virtuale con un'immagine di macchina virtuale contenente alcuni software pre-installato, aggiuntive oraria software potrebbero essere addebitati. Azure addebita separatamente per l'archiviazione del sistema operativo della macchina virtuale di hello e i dischi dati. L’archiviazione su disco temporaneo è gratuita.

Vengono addebitati quando hello stato della macchina virtuale è in esecuzione o arrestato, ma non vengono addebitate quando hello stato della macchina virtuale viene arrestata (deallocata). una macchina virtuale in hello tooput arrestato (deallocato), effettuare una delle seguenti hello:

* Arrestare o eliminare hello macchina virtuale dal portale di Azure classico hello.
* Utilizzare i cmdlet Stop-AzureVM hello, disponibile nel modulo Azure PowerShell hello.
* Utilizzare l'operazione di arresto del ruolo hello in hello API REST di gestione e specificare StoppedDeallocated per l'elemento PostShutdownAction hello.

Per informazioni dettagliate, vedere [Prezzi delle macchine virtuali](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="will-azure-reboot-my-vm-for-maintenance"></a>Azure riavvia la VM per manutenzione?
Azure talvolta riavvia la macchina virtuale come parte degli aggiornamenti di manutenzione pianificata regolari in hello Data Center di Azure.

Gli eventi di manutenzione non pianificati possono verificarsi quando Azure rileva un problema hardware grave che interessa la VM. Per gli eventi non pianificati, Azure automaticamente viene eseguita la migrazione di host di hello VM tooa integro e riavvia hello macchina virtuale.

Per qualsiasi macchina virtuale autonoma, ovvero hello VM non fa parte di un set di disponibilità, Azure notifica all'amministratore del servizio della sottoscrizione hello tramite posta elettronica almeno una settimana prima della manutenzione pianificata perché può essere riavviata hello macchine virtuali durante l'aggiornamento di hello. Le applicazioni in esecuzione nelle macchine virtuali hello potrebbe subire tempi di inattività.

È inoltre possibile utilizzare hello portale di Azure classico o log di Azure PowerShell tooview hello riavvio quando si è verificato il riavvio di hello scadenza tooplanned manutenzione. Per informazioni dettagliate, vedere [Visualizzazione dei registri di riavvio della macchina virtuale](https://azure.microsoft.com/blog/2015/04/01/viewing-vm-reboot-logs/).

tooprovide ridondanza, inserire due o più simili configurato le macchine virtuali in hello stesso set di disponibilità. In questo modo si assicura che almeno una VM sia disponibile durante la manutenzione pianificata o non pianificata. Azure garantisce determinati livelli di disponibilità della VM per questa configurazione. Per informazioni dettagliate, vedere [gestione hello disponibilità delle macchine virtuali](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="additional-resources"></a>Risorse aggiuntive
[Informazioni sulle macchine virtuali di Azure](../articles/virtual-machines/virtual-machines-linux-about.md)

[Creare e gestire le macchine virtuali Linux con hello CLI di Azure](../articles/virtual-machines/linux/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Creare e gestire VM Windows con Azure PowerShell](../articles/virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

