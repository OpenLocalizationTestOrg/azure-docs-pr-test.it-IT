# <a name="platform-supported-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Piattaforma supportata la migrazione di risorse IaaS tooAzure classico Gestione risorse
In questo articolo viene descritto come si abilita la migrazione dell'infrastruttura come un servizio (IaaS) alle risorse da modelli di distribuzione di gestione di hello Classic tooResource. Altre informazioni su [funzionalità e vantaggi di Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md). È in dettaglio come risorse tooconnect hello due modelli di distribuzione che coesistono nella sottoscrizione tramite virtuale site-to-site gateway di rete.

## <a name="goal-for-migration"></a>Obiettivo della migrazione
Resource Manager consente di distribuire applicazioni complesse mediante modelli, configura le macchine virtuali tramite le estensioni di macchina virtuale e incorpora la gestione degli accessi e l'uso dei tag. Azure Resource Manager include anche una distribuzione parallela e scalabile per le macchine virtuali nei set di disponibilità. il nuovo modello di distribuzione Hello fornisce inoltre la gestione del ciclo di vita di calcolo, rete e archiviazione in modo indipendente. Infine, è disponibile un stato attivo sull'abilitazione della protezione per impostazione predefinita con l'applicazione hello di macchine virtuali in una rete virtuale.

Quasi tutte le funzionalità di hello del modello di distribuzione classica hello sono supportate per calcolo, rete e archiviazione in Azure Resource Manager. toobenefit da nuove funzionalità di hello in Gestione risorse di Azure, è possibile migrare le distribuzioni dal modello di distribuzione classica hello esistente.

## <a name="supported-resources-for-migration"></a>Risorse supportate per la migrazione
Durante la migrazione sono supportate queste risorse IaaS classiche

* Macchine virtuali
* SET DI DISPONIBILITÀ
* Servizi cloud
* Account di archiviazione
* Reti virtuali
* Gateway VPN
* Express Route gateway _(in hello stessa sottoscrizione di rete virtuale solo)_
* Gruppi di sicurezza di rete 
* Tabelle di route 
* IP riservati 

## <a name="supported-scopes-of-migration"></a>Ambiti di migrazione supportati
Esistono diversi 4 modi toocomplete migrazione delle risorse di calcolo, rete e archiviazione. Si tratta di 

* Migrazione di macchine virtuali (NON in una rete virtuale)
* Migrazione di macchine virtuali (in una rete virtuale)
* Migrazione degli account di archiviazione
* Risorse scollegate (gruppi di sicurezza di rete, tabelle di route e indirizzi IP riservati)

### <a name="migration-of-virtual-machines-not-in-a-virtual-network"></a>Migrazione di macchine virtuali (NON in una rete virtuale)
Nel modello di distribuzione di gestione risorse hello, protezione viene applicata per le applicazioni per impostazione predefinita. Tutte le macchine virtuali è necessario toobe in una rete virtuale nel modello di gestione risorse di hello. piattaforma Azure riavvii Hello (`Stop`, `Deallocate`, e `Start`) hello macchine virtuali come parte della migrazione hello. Per le reti virtuali hello che hello macchine virtuali vengono migrate, sono disponibili due opzioni:

* È possibile richiedere hello piattaforma toocreate una nuova rete virtuale e la migrazione di macchina virtuale hello nella nuova rete virtuale hello.
* È possibile eseguire la migrazione di macchina virtuale hello in una rete virtuale esistente in Gestione risorse.

> [!NOTE]
> In questo ambito, la migrazione entrambi hello operazioni del piano di gestione e operazioni del piano dati hello possono non essere consentite per un periodo di tempo durante la migrazione di hello.
>
>

### <a name="migration-of-virtual-machines-in-a-virtual-network"></a>Migrazione di macchine virtuali (in una rete virtuale)
Per la maggior parte delle configurazioni di macchina virtuale, solo i metadati di hello sta migrando tra modelli di distribuzione classica e Gestione risorse di hello. Hello sottostante macchine virtuali in esecuzione su hello dello stesso hardware, in hello stessa rete e con hello stessa archiviazione. le operazioni di gestione piano Hello possono non essere consentite per un determinato periodo di tempo durante la migrazione di hello. Tuttavia, il piano di dati hello continua toowork. Ovvero, le applicazioni in esecuzione su macchine virtuali (classiche) non comportano un tempo di inattività durante la migrazione di hello.

Hello seguenti configurazioni non è attualmente supportato. Se viene aggiunto il supporto in futuro hello alcune macchine virtuali in questa configurazione potrebbe essere addebitato un tempo di inattività (passare tramite stop, rilasciare e riavviare le operazioni di VM).

* Un singolo servizio cloud include più di un set di disponibilità.
* In un singolo servizio cloud sono presenti uno o più set di disponibilità e VM non incluse in un set di disponibilità.

> [!NOTE]
> In questo ambito di migrazione, il piano di gestione di hello può non essere consentito per un periodo di tempo durante la migrazione di hello. Per alcune configurazioni, come illustrato in precedenza, il piano dati subisce tempi di inattività.
>
>

### <a name="storage-accounts-migration"></a>Migrazione degli account di archiviazione
migrazione continua tooallow, è possibile distribuire macchine virtuali di gestione risorse in un account di archiviazione classico. Questa funzionalità consente di eseguire la migrazione di risorse di calcolo e di rete indipendentemente dagli account di archiviazione. Quando si esegue la migrazione tramite le macchine virtuali e rete virtuale, sarà necessario toomigrate tramite il processo di migrazione hello toocomplete gli account di archiviazione.

> [!NOTE]
> modello di distribuzione di gestione risorse di Hello non hanno il concetto di hello di classica immagini e dischi. Quando l'account di archiviazione hello viene migrate, classiche immagini e dischi non sono visibili in stack di Resource Manager hello ma hello backup dischi rigidi virtuali rimangono nell'account di archiviazione hello.
>
>

### <a name="unattached-resources-network-security-groups-route-tables--reserved-ips"></a>Risorse scollegate (gruppi di sicurezza di rete, tabelle di route e indirizzi IP riservati)
Gruppi di sicurezza di rete, le tabelle di Route e gli indirizzi IP riservati non sono collegati tooany macchine virtuali e reti virtuali possono essere migrate in modo indipendente.

<br>

## <a name="unsupported-features-and-configurations"></a>Funzionalità e configurazioni non supportate
Alcune funzionalità e configurazioni non sono attualmente supportate. Hello le sezioni seguenti vengono descritti questi consigli attorno a esse.

### <a name="unsupported-features"></a>Funzionalità non supportate
Hello seguenti caratteristiche non è attualmente supportato. È facoltativamente rimuovere queste impostazioni, eseguire la migrazione di macchine virtuali hello e quindi abilitare nuovamente le impostazioni di hello nel modello di distribuzione di gestione risorse di hello.

| Provider di risorse | Funzionalità | Raccomandazione |
| --- | --- | --- |
| Calcolo |Dischi di macchine virtuali non associati. | BLOB VHD Hello protetti da tali dischi verranno ottenere migrati quando viene eseguita la migrazione di Account di archiviazione hello |
| Calcolo |Immagini di macchine virtuali. | BLOB VHD Hello protetti da tali dischi verranno ottenere migrati quando viene eseguita la migrazione di Account di archiviazione hello |
| Rete |ACL endpoint. | Rimuovere gli ACL endpoint e ripetere la migrazione. |
| Rete |Rete virtuale con gateway ExpressRoute e gateway VPN.  | Rimuovere hello Gateway VPN prima di iniziare la migrazione e quindi ricreare hello Gateway VPN una volta completata la migrazione. Per altre informazioni, vedere l'articolo relativo alla [migrazione di ExpressRoute](../articles/expressroute/expressroute-migration-classic-resource-manager.md).|
| Rete |ExpressRoute con collegamenti di autorizzazione.  | Rimuovere hello ExpressRoute circuito toovirtaul connessione di rete prima di iniziare la migrazione e quindi ricreare la connessione hello una volta completata la migrazione. Per altre informazioni, vedere l'articolo relativo alla [migrazione di ExpressRoute](../articles/expressroute/expressroute-migration-classic-resource-manager.md). |
| Rete |gateway applicazione | Rimuovere hello Gateway applicazione prima di iniziare la migrazione e quindi ricreare il Gateway applicazione hello una volta completata la migrazione. |
| Rete |Reti virtuali usando il peering delle reti virtuali. | Eseguire la migrazione di rete virtuale tooResource Manager, quindi peer. Altre informazioni sul [peering reti virtuali](../articles/virtual-network/virtual-network-peering-overview.md). | 

### <a name="unsupported-configurations"></a>Configurazioni non supportate
Hello seguenti configurazioni non è attualmente supportato.

| Service | Configurazione | Raccomandazione |
| --- | --- | --- |
| Gestione risorse |Controllo degli accessi in base al ruolo (RBAC) per le risorse classiche |Poiché hello URI delle risorse hello viene modificato dopo la migrazione, è consigliabile pianificare gli aggiornamenti di criteri RBAC hello necessarie toohappen dopo la migrazione. |
| Calcolo |Più subnet associate a una macchina virtuale |Subnet tooreference di configurazione subnet hello solo l'aggiornamento. |
| Calcolo |Macchine virtuali che fanno parte di rete virtuale tooa ma non dispone di una subnet esplicita assegnata |Facoltativamente, è possibile eliminare hello macchina virtuale. |
| Calcolo |Macchine virtuali con avvisi e criteri di ridimensionamento automatico |migrazione di Hello attraversa e queste impostazioni vengono eliminate. È consigliabile valutare l'ambiente prima hello migrazione. In alternativa, è possibile riconfigurare le impostazioni degli avvisi di hello al termine della migrazione. |
| Calcolo |Estensioni XML della VM (BGInfo 1.*, Visual Studio Debugger, Web Deploy e Remote Debugging) |Questa operazione non è supportata. È consigliabile che per rimuovere queste estensioni toocontinue migrazione della macchina virtuale hello o verranno eliminati automaticamente durante il processo di migrazione hello. |
| Calcolo |Diagnostica di avvio con archiviazione Premium |Disabilitare la funzionalità di diagnostica di avvio per le macchine virtuali hello prima di continuare con la migrazione. È possibile riabilitare la diagnostica di avvio nello stack di Resource Manager hello al termine della migrazione hello. Inoltre, i BLOB in uso per le schermate e i registri seriali devono essere eliminati in modo da non ricevere addebiti in relazione a essi. |
| Calcolo |Servizi cloud che includono ruoli Web/di lavoro |Non supportato attualmente. |
| Rete |Reti virtuali contenenti macchine virtuali e ruoli Web/di lavoro |Non supportato attualmente. |
| Servizio app di Azure |Rete virtuale contenente ambienti del servizio app |Non supportato attualmente. |
| HDInsight di Azure |Rete virtuale contenente servizi HDInsight |Non supportato attualmente. |
| Servizi del ciclo di vita Microsoft Dynamics |Rete virtuale contenente macchine virtuali gestite da Dynamics Lifecycle Services |Non supportato attualmente. |
| Servizi di dominio Azure Active Directory |Reti virtuali che contengono i servizi di dominio Azure AD |Non supportato attualmente. |
| Azure RemoteApp |Reti virtuali che contengono distribuzioni di Azure RemoteApp |Non supportato attualmente. |
| Gestione API di Azure |Reti virtuali che contengono distribuzioni di Gestione API |Non supportato attualmente. hello toomigrate VNET IaaS, modificare hello rete virtuale di hello la distribuzione di gestione API che non è un'operazione alcun tempo di inattività. |
| Calcolo |Estensioni del Centro sicurezza di Azure con una rete virtuale che dispone di un gateway VPN in connettività di transito o ExpressRoute con server DNS locale |Centro sicurezza di Azure automaticamente installati estensioni toomonitor le macchine virtuali la sicurezza e generare avvisi. Queste estensioni in genere viene installate automaticamente se è abilitato hello criteri Centro sicurezza di Azure nella sottoscrizione hello. La migrazione del gateway ExpressRoute non è attualmente supportata e i gateway VPN con connettività di transito perdono l'accesso locale. L'eliminazione di ExpressRoute gateway o la migrazione dei gateway VPN con connettività di transito determina internet access tooVM storage account toobe perdita quando procedere all'esecuzione del commit della migrazione hello. la migrazione di Hello non viene eseguita in questo caso come blob di stato dell'agente guest hello non possono essere popolati. È consigliabile toodisable criteri Centro sicurezza di Azure nella sottoscrizione hello 3 ore prima di procedere con la migrazione. |

