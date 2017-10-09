## <a name="meaning-of-migration-of-iaas-resources-from-hello-classic-deployment-model-tooresource-manager"></a>Significato della migrazione di risorse IaaS tooResource modello di distribuzione classica hello Manager
Prima abbiamo drill-down dei dettagli di hello, esaminiamo differenza hello tra dati piano e di Gestione operazioni su risorse IaaS hello.

* *Piano di gestione e controllo* descrive chiamate hello che vengono immessi nel piano di gestione e controllo hello o hello API per la modifica delle risorse. Ad esempio, operazioni come la creazione di una macchina virtuale, riavviare una macchina virtuale e l'aggiornamento di una rete virtuale con una nuova subnet gestire hello in risorse di esecuzione. Essi non influiscono direttamente sulla connessione toohello istanze.
* *Piano dati* (applicazione) descrive hello runtime dell'applicazione hello e comporta l'interazione con le istanze che non passano attraverso hello API di Azure. L'accesso al sito Web o il pull dei dati da un'istanza di SQL Server o da un server mongoDB in esecuzione verranno considerati parte del piano dati o dell'interazione con l'applicazione. Copia un blob da un account di archiviazione e l'accesso a un pubblico tooRDP indirizzo IP o SSH nella macchina virtuale hello sono anche piano dati. Queste operazioni mantengono un'applicazione hello calcolo, rete e archiviazione in esecuzione.

Dietro le quinte hello piano dati hello è hello stesso tra il modello di distribuzione classica hello e stack Resource Manager. Durante il processo di migrazione, si conversione rappresentazione hello delle risorse di hello da hello Classic distribuzione modello toothat nello stack di Resource Manager hello. Di conseguenza, sarà necessario toouse nuovi strumenti e API SDK toomanage le risorse nello stack di Resource Manager hello.

![Screenshot che illustra la differenza tra piano di gestione/controllo e piano dati](../articles/virtual-machines/media/virtual-machines-windows-migration-classic-resource-manager/data-control-plane.png)


> [!NOTE]
> In alcuni scenari di migrazione, hello piattaforma Azure arresta dealloca e riavvia le macchine virtuali. Questa operazione comporta brevi tempi di inattività del piano dati.
>

## <a name="hello-migration-experience"></a>esperienza di migrazione Hello
Prima di iniziare l'esperienza di migrazione hello, hello è consigliabile:

* Assicurarsi che non utilizzino risorse hello che si desidera toomigrate eventuali configurazioni o una funzionalità non supportate. In genere piattaforma hello rileva questi problemi e genera un errore.
* Se si dispone di macchine virtuali che non sono presenti in una rete virtuale, essi verrà arrestati e DEALLOCATE come parte di hello l'operazione di preparazione. Se non si desidera l'indirizzo IP pubblico di toolose hello, esaminare la prenotazione di indirizzo IP di hello prima che venga attivato hello l'operazione di preparazione. Tuttavia, se le macchine virtuali hello in una rete virtuale, non sono arrestate e DEALLOCATE.
* Pianificare la migrazione durante le ore non lavorative tooaccommodate per individuare eventuali guasti imprevisti che possono verificarsi durante la migrazione.
* Scaricare la configurazione corrente di hello delle macchine virtuali con PowerShell, i comandi dell'interfaccia della riga di comando (CLI) o le API REST toomake più semplice per la convalida dopo il passaggio di preparazione hello è stata completata.
* Prima di iniziare la migrazione di hello, aggiornare il modello di distribuzione automazione/rendere operativo script toohandle hello Gestione risorse. Facoltativamente, è possibile eseguire le operazioni GET caso hello risorse hello stato preparato.
* Valutare i criteri RBAC hello che sono configurati su risorse IaaS classiche hello e piano al termine della migrazione hello.

flusso di lavoro migrazione Hello è indicato di seguito

![Schermata che mostra il flusso di migrazione hello](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-workflow.png)

> [!NOTE]
> Tutte le operazioni descritte nelle sezioni che seguono hello hello sono idempotenti. Se si dispone di un problema diverso da una funzionalità non supportata o un errore di configurazione, è consigliabile che si riprova hello preparare, interrompere o l'operazione di commit. Hello piattaforma Azure tenta di nuovo l'azione hello.
>
>

### <a name="validate"></a>Convalida
operazione di convalida Hello è hello primo passaggio nel processo di migrazione hello. obiettivo di Hello di questo passaggio è stato hello tooanalyze delle risorse di hello si desidera toomigrate nel modello di distribuzione classica hello e restituisce l'esito positivo o negativo se le risorse di hello sono in grado di migrazione.

Selezionare la rete virtuale hello o un servizio cloud (se non è in una rete virtuale) che si desidera toovalidate per la migrazione.

* Se la risorsa hello non è in grado di migrazione, hello piattaforma Azure vengono elencate tutte le cause hello perché non è supportata per la migrazione.

#### <a name="checks-not-done-in-validate"></a>Verifiche non eseguite nella convalida

Convalidare operazione analizza solo stato hello delle risorse di hello nel modello di distribuzione classica hello. È possibile cercare tutti gli scenari non supportati a causa delle configurazioni toovarious nel modello di distribuzione classica hello. Non è possibile toocheck per tutti i problemi che hello Azure Resource Manager stack imponga risorse hello durante la migrazione. Questi problemi vengono controllati solo quando le risorse di hello subiscono trasformazione nel passaggio successivo hello della migrazione, vale a dire, preparazione. tabella Hello riportata di seguito sono elencati tutti i problemi di hello non è selezionati nella convalida.


|Controlli di rete non eseguiti nella convalida|
|-|
|Rete virtuale con gateway ExpressRoute e VPN|
|Connessione gateway di rete virtuale in stato disconnesso|
|Tutti i circuiti Expressroute sono pre-migrati tooAzure stack di Resource Manager|
|Verifica della quota di Azure Resource Manager per le risorse di rete, vale a dire l'indirizzo IP pubblico statico, gli indirizzi IP pubblici dinamici, Load Balancer, i gruppi di sicurezza di rete, le tabelle di routing e le interfacce di rete |
| Verifica che tutte le regole del servizio di bilanciamento del carico siano valide nella distribuzione e nella rete virtuale |
| Verificare la presenza di indirizzi IP privati in conflitto tra macchine virtuali arrestate DEALLOCATE in hello stessa rete virtuale |

### <a name="prepare"></a>Preparazione
l'operazione di preparazione Hello rappresenta hello secondo passaggio del processo di migrazione hello. obiettivo di Hello di questo passaggio è trasformazione hello toosimulate di hello le risorse IaaS da Gestione risorse tooResource del modello di distribuzione classica e presentano questo side-by-side è toovisualize.

> [!NOTE] 
> Le risorse del modello di distribuzione classica non vengono modificate in questo passaggio. È un toorun passaggio sicura se si sta tentando di fuori della migrazione. 

Selezionare servizio cloud hello o di rete virtuale hello (se non si tratta di una rete virtuale) che si desidera tooprepare per la migrazione.

* Risorsa hello non è in grado di migrazione, hello piattaforma Azure Arresta il processo di migrazione hello elenchi e il motivo di hello perché hello preparare l'operazione non riuscita.
* Se la risorsa hello è in grado di migrazione, hello piattaforma Azure protegge innanzitutto le operazioni di gestione piano hello per le risorse di hello in fase di migrazione. Ad esempio, non sono in grado di tooadd un tooa di disco dati macchina virtuale in fase di migrazione.

Hello piattaforma Azure quindi avvia hello migrazione dei metadati dal modello di distribuzione classica tooResource Manager per la migrazione di risorse hello.

Dopo la preparazione hello operazione è stata completata, è possibile hello visualizzazione risorse hello sia il modello di distribuzione classica e Gestione risorse. Per ogni servizio cloud nel modello di distribuzione classica hello, hello piattaforma Azure crea un nome di gruppo di risorse con il modello di hello `cloud-service-name>-Migrated`.

> [!NOTE]
> Possibili tooselect hello nome del gruppo di risorse creati per le risorse migrate non è (ad esempio "-migrati") ma al termine della migrazione, è possibile utilizzare Gestione risorse di Azure Sposta funzionalità toomove risorse tooany gruppo di risorse desiderato. altre informazioni, vedi tooread [spostare sottoscrizione o il gruppo di risorse toonew risorse](../articles/resource-group-move-resources.md)

Di seguito sono due schermate che illustrano il risultato di hello dopo un'operazione di preparazione di seguito. Prima schermata viene visualizzato un gruppo di risorse contenente hello originale del servizio cloud. Seconda schermata mostra nuova hello "-migrati" gruppo di risorse che contiene le risorse di gestione risorse di Azure equivalente hello.

![Schermata che mostra il servizio cloud classico del portale](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-classic.png)

![Schermata che mostra le risorse Azure Resource Manager del portale in preparazione](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-arm.png)

Ecco alcuni esaminare le risorse dopo il completamento della fase di preparazione hello. Si noti che la risorsa hello piano dati hello è hello stesso. Viene rappresentato in sia hello gestione piano (modello di distribuzione classica) e di hello controllo Gestione risorse ().

![Background hello in fase di preparazione](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-prepare.png)

> [!NOTE]
> Le macchine virtuali che non sono in una rete virtuale classica vengono interrotte e deallocate in questa fase della migrazione.
>

### <a name="check-manual-or-scripted"></a>Verifica (manuale o tramite script)
Nel passaggio di controllo hello, è possibile utilizzare facoltativamente configurazione hello scaricato toovalidate precedente che la migrazione di hello siano corretta. In alternativa, è possibile accedere toohello portale e controllo hello proprietà e risorse toovalidate che la migrazione dei metadati ha esito positivo.

Se si esegue la migrazione di una rete virtuale, la maggior parte delle configurazioni delle macchine virtuali non viene riavviata. Per le applicazioni su tali macchine virtuali, è possibile convalidare che un'applicazione hello sia ancora in esecuzione.

È possibile verificare il monitoraggio o di automazione e script operativi toosee se hello macchine virtuali funzionino come previsto e se gli script aggiornati funziona correttamente. Quando le risorse di hello sono in stato preparato hello, sono supportate solo operazioni GET.

Non vi è alcun intervallo di tempo set prima della quale è necessario eseguire una migrazione hello toocommit. In questo stato non sono previsti limiti di tempo. Tuttavia, il piano di gestione di hello è bloccato per tali risorse finché non viene interrotta oppure eseguire il commit.

Se i problemi, è possibile interrompere la migrazione di hello e tornare al modello di distribuzione classica toohello. Quando si torna indietro, hello piattaforma Azure aprirà operazioni di gestione piano hello sulle risorse di hello in modo che è possibile riprendere le normali operazioni su tali macchine virtuali nel modello di distribuzione classica hello.

### <a name="abort"></a>Interruzione
L'interruzione è un passaggio facoltativo che è possibile utilizzare il modello di distribuzione classica toohello modifiche di toorevert e interrompere la migrazione di hello. Questa operazione Elimina i metadati di gestione risorse per le risorse che è stato creato nel passaggio di preparazione precedente hello hello. 

![Background hello in fase di interruzione](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-abort.png)


> [!NOTE]
> Questa operazione non può essere eseguita dopo che si have attivato l'operazione di commit hello.     
>

### <a name="commit"></a>Commit
Al termine della convalida hello, è possibile eseguire il commit della migrazione hello. Le risorse non viene più visualizzato nel modello di distribuzione classica e sono disponibili solo nel modello di distribuzione di gestione risorse di hello. Hello risorse migrate possono essere gestite solo nel nuovo portale di hello.

> [!NOTE]
> Si tratta di un'operazione idempotente. In caso contrario, è consigliabile che ripetere l'operazione di hello. Se continua a toofail, creare un ticket di supporto o creare un forum post con un tag di ClassicIaaSMigration nostri [forum VM](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).
>
>

![Background hello in fase di Commit](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-commit.png)

## <a name="where-toobegin-migration"></a>In migrazione toobegin?

Ecco un diagramma di flusso che illustra come tooproceed con la migrazione

![Schermata che illustra i passaggi della migrazione hello](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="translation-of-classic-deployment-model-tooazure-resource-manager-resources"></a>Conversione di risorse di gestione delle risorse tooAzure del modello di distribuzione classica
È possibile trovare il modello di distribuzione classica hello e rappresentazioni di gestione risorse di risorse hello in hello nella tabella seguente. Le seguenti funzionalità e risorse non sono attualmente supportate.

| Rappresentazione classica | Rappresentazione in Resource Manager | Note dettagliate |
| --- | --- | --- |
| Nome del servizio cloud |Nome DNS |Durante la migrazione, viene creato un nuovo gruppo di risorse per ogni servizio cloud con modello di denominazione hello `<cloudservicename>-migrated`. Questo gruppo di risorse contiene tutte le risorse. nome del servizio cloud Hello diventa un nome DNS associato a indirizzo IP pubblico hello. |
| Macchina virtuale |Macchina virtuale |Le proprietà specifiche della VM vengono migrate senza variazioni. Alcune informazioni osProfile, come nome del computer, non viene archiviate nel modello di distribuzione classica hello e rimangono vuoti dopo la migrazione. |
| Le risorse disco collegato tooVM |TooVM implicita dischi collegati |I dischi non vengono modellati come risorse di livello superiore nel modello di distribuzione di gestione risorse di hello. Esse vengono migrate come dischi impliciti in hello macchina virtuale. Solo i dischi che sono collegati tooa VM sono attualmente supportati. Macchine virtuali di gestione delle risorse possono ora utilizzare gli account di archiviazione classico, che consente di hello dischi toobe facilmente la migrazione senza aggiornamenti. |
| Estensioni di VM |Estensioni di VM |Vengono eseguita la migrazione di tutte le estensioni risorsa hello, ad eccezione delle estensioni XML, dal modello di distribuzione classica hello. |
| Certificati di macchine virtuali |Certificati nell'insieme di credenziali delle chiavi di Azure |Se un servizio cloud contiene i certificati di servizio, un nuovo archivio di chiavi di Azure per il servizio cloud e sposta i certificati di hello nell'insieme di credenziali chiave hello. macchine virtuali Hello sono certificati hello tooreference aggiornata dall'insieme di credenziali chiave hello. <br><br> **Nota:** non eliminare keyvault hello in quanto può provocare toogo VM hello in uno stato di errore. Stiamo lavorando su come migliorare operazioni nel back-end hello in modo che gli insiemi di credenziali chiave può essere eliminati o spostati insieme hello nuova sottoscrizione di VM tooa. |
| Configurazione di WinRM |Configurazione di WinRM in osProfile |Spostamento di configurazione di gestione remota Windows invariato, come parte della migrazione hello. |
| Proprietà del set di disponibilità |Risorsa del set di disponibilità | Specifica di set di disponibilità è una proprietà nel modello di distribuzione classica hello Ciao VM. Set di disponibilità diventano una risorsa di primo livello come parte della migrazione hello. Hello configurazioni seguenti non sono supportate: più gruppi di disponibilità per il servizio cloud o set di disponibilità di uno o più insieme a macchine virtuali che non si trovano in qualsiasi set di disponibilità in un servizio cloud. |
| Configurazione di rete in una VM |Interfaccia di rete primaria |Configurazione di rete in una macchina virtuale viene rappresentata come risorse di interfaccia di rete primaria hello dopo la migrazione. Per le macchine virtuali che non sono presenti in una rete virtuale, l'indirizzo IP interno hello cambia durante la migrazione. |
| Più interfacce di rete in una VM |Interfacce di rete |Se una macchina virtuale dispone di più interfacce di rete associate, ogni interfaccia di rete diventa una risorsa di primo livello come parte della migrazione hello nel modello di distribuzione di gestione delle risorse di hello, insieme a tutte le proprietà di hello. |
| Set di endpoint con carico bilanciato |Bilanciamento del carico |Nel modello di distribuzione classica hello, piattaforma hello assegnato a un servizio di bilanciamento del carico implicito per ogni servizio cloud. Durante la migrazione, viene creata una nuova risorsa di bilanciamento del carico e set di endpoint con bilanciamento del carico hello diventa regole di bilanciamento del carico. |
| Regole NAT in ingresso |Regole NAT in ingresso |Gli endpoint di input definiti nell'hello VM sono regole di tooinbound convertito network address translation nel servizio di bilanciamento del carico hello durante la migrazione di hello. |
| Indirizzo VIP |Indirizzo IP pubblico con nome DNS |indirizzo IP virtuale Hello diventa un indirizzo IP pubblico e associata a bilanciamento del carico hello. Un indirizzo IP virtuale può essere eseguito solo se è presente un endpoint di input tooit assegnato. |
| Rete virtuale |Rete virtuale |rete virtuale Hello viene eseguita la migrazione, con tutte le relative proprietà, modello di distribuzione di gestione risorse toohello. Viene creato un nuovo gruppo di risorse con nome hello `-migrated`. |
| IP riservati |Indirizzo IP pubblico con allocationMethod statico |Gli indirizzi IP riservati associato a bilanciamento del carico hello vengono migrate, insieme a migrazione hello del servizio cloud hello o una macchina virtuale hello. La migrazione di indirizzi IP riservati non associati non è attualmente supportata. |
| Indirizzo IP pubblico per VM |Indirizzo IP pubblico con Allocationmethod dinamico |Hello indirizzo IP pubblico associato alla macchina virtuale viene convertito come una risorsa di indirizzo IP pubblica, con hello allocazione metodo set toostatic hello. |
| Gruppi di sicurezza di rete |Gruppi di sicurezza di rete |Come parte del modello di distribuzione di gestione risorse di hello migrazione toohello vengono clonati i gruppi di sicurezza di rete associati a una subnet. Hello gruppo nel modello di distribuzione classica hello non viene rimosso durante la migrazione di hello. Tuttavia, le operazioni di gestione piano hello per hello NSG vengono bloccate quando è in corso la migrazione di hello. |
| Server DNS |Server DNS |I server DNS è associata a una rete virtuale o hello VM vengono migrate come parte di hello corrispondente la migrazione di risorse, insieme a tutte le proprietà di hello. |
| Route definite dall'utente |Route definite dall'utente |Le route definite dall'utente associate a una subnet vengono clonate come parte del modello di distribuzione di gestione risorse di hello migrazione toohello. Hello UDR nel modello di distribuzione classica hello non viene rimosso durante la migrazione di hello. operazioni di gestione piano Hello per hello UDR vengono bloccate quando è in corso la migrazione di hello. |
| Proprietà di inoltro IP nella configurazione di rete di una VM |Proprietà hello NIC inoltro dell'indirizzo IP |proprietà di inoltro dell'indirizzo IP Hello in una macchina virtuale è convertito tooa proprietà nell'interfaccia di rete hello durante la migrazione di hello. |
| Servizio di bilanciamento del carico con più IP |Servizio di bilanciamento del carico con più risorse IP pubblico |Ogni indirizzo IP pubblico associato al servizio di bilanciamento del carico hello è risorsa IP pubblica tooa convertito e associata a bilanciamento del carico hello dopo la migrazione. |
| Nomi DNS interni nella VM hello |Nomi DNS interni nella hello NIC |Durante la migrazione, suffissi DNS interni hello per le macchine virtuali hello sono proprietà di sola lettura di tooa migrati denominata "InternalDomainNameSuffix" su hello scheda di rete. suffisso Hello rimane invariata dopo la migrazione e la risoluzione di macchina virtuale deve continuare toowork come in precedenza. |
| Gateway di rete virtuale |Gateway di rete virtuale |Le proprietà del gateway di rete virtuali restano invariate durante la migrazione, Hello VIP associato hello gateway non subirà alcuna modifica. |
| Sito di rete locale |Gateway di rete locale |Proprietà del sito di rete locale sono migrati tooa invariato nuova risorsa denominata Gateway di rete locale. che rappresenta i prefissi degli indirizzi locali e l'IP del gateway remoto. |
| Riferimenti alle connessioni |Connessione |I riferimenti alla connettività tra il gateway e il sito di rete locale nella configurazione di rete sono rappresentati da una risorsa appena creata e denominata Connessione in Resource Manager dopo la migrazione. Tutte le proprietà di riferimento di connettività nei file di configurazione di rete sono una risorsa di connessione copiato toohello invariato appena creato. Connettività di rete virtuale tooVNet classica è possibile creare due tunnel IPsec toolocal siti di rete che rappresenta hello reti virtuali. Connessione tooVnet2Vnet trasformato tipo nel modello di gestione delle risorse senza gateway di rete locale. |

## <a name="changes-tooyour-automation-and-tooling-after-migration"></a>Automazione tooyour modifiche e gli strumenti al termine della migrazione
Come parte della migrazione delle risorse da modello di distribuzione di hello Classic distribuzione modello toohello Gestione risorse, è necessario tooupdate l'automazione esistente o tooensure gli strumenti che continui toowork dopo la migrazione di hello.
