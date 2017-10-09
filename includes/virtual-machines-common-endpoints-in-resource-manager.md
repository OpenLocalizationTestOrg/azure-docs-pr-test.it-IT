gli endpoint di Hello approccio tooAzure funzionamento è leggermente diverso tra i modelli di distribuzione classica e Gestione risorse hello. Nel modello di distribuzione di gestione risorse hello, si dispongono di hello flessibilità toocreate rete filtri controllano hello flusso del traffico da e verso le macchine virtuali. Questi filtri consentono di toocreate complesso negli ambienti di rete oltre a un endpoint di tipo semplice come modello di distribuzione classica hello. Questo articolo offre una panoramica dei gruppi di sicurezza di rete, delle differenze rispetto all'uso degli endpoint del modello di distribuzione classica, della creazione di regole di filtro e di scenari di distribuzione di esempio.

## <a name="overview-of-resource-manager-deployments"></a>Panoramica delle distribuzioni Resource Manager
Gli endpoint nel modello di distribuzione classica hello vengono sostituiti da gruppi di sicurezza di rete e le regole di controllo elenco (ACL) di accesso. Le azioni rapide per implementare le regole ACL dei gruppi di sicurezza di rete sono le seguenti:

* Creare un gruppo di sicurezza di rete.
* tooallow o negare il traffico, definire le regole ACL gruppo di sicurezza rete.
* Assegnare l'interfaccia di rete tooa il gruppo di sicurezza di rete o subnet della rete virtuale.

Se si sono che desiderano tooalso eseguire l'inoltro alla porta, è necessario tooplace un bilanciamento del carico davanti la macchina virtuale e utilizzare le regole NAT. Le azioni rapide per implementare un servizio di bilanciamento del carico e regole NAT saranno le seguenti:

* Creare un servizio di bilanciamento del carico.
* Creare un pool back-end e aggiungere il pool di toohello macchine virtuali.
* Definire le regole NAT per inoltro alla porta hello necessario.
* Assegnare le regole NAT tooyour VM.

## <a name="network-security-group-overview"></a>Panoramica dei gruppi di sicurezza di rete
Gruppi di sicurezza di rete forniscono un livello di protezione per l'utente tooallow determinate porte e subnet tooaccess le macchine virtuali. In genere è sempre un gruppo di sicurezza di rete che fornisce il livello di sicurezza tra le macchine virtuali e hello world di fuori. Gruppi di sicurezza di rete può essere applicato tooa subnet della rete virtuale o un'interfaccia di rete specifico per una macchina virtuale. Invece di creare regole ACL di endpoint, si creano le regole ACL dei gruppi di sicurezza di rete. Queste regole ACL consentono di controllare maggiore rispetto alla creazione di un endpoint tooforward semplicemente una determinata porta. Per altre informazioni, vedere [Informazioni sui gruppi di sicurezza di rete](../articles/virtual-network/virtual-networks-nsg.md).

> [!TIP]
> È possibile assegnare le subnet toomultiple gruppi di sicurezza di rete o interfacce di rete. Non esiste un mapping 1:1. È possibile creare un gruppo di sicurezza di rete con un set comune di regole ACL e applicare toomultiple subnet o le interfacce di rete. Inoltre, il gruppo di sicurezza di rete può essere applicato tooresources tra la sottoscrizione (in base a [i controlli di accesso basato su ruolo](../articles/active-directory/role-based-access-control-what-is.md).

## <a name="load-balancers-overview"></a>Panoramica dei servizi di bilanciamento del carico
Nel modello di distribuzione classica hello, Azure potrebbe eseguire hello tutti Network Address Translation (NAT) e inoltro in un servizio Cloud per consentire alla porta. Quando si crea un endpoint, è necessario specificare hello porta esterna tooexpose insieme hello porta interna toodirect traffico. I gruppi di sicurezza di rete non eseguono autonomamente le stesse operazioni NAT e di port forwarding. 

tooallow le regole NAT toocreate per tale porta di inoltro, creare un servizio di bilanciamento del carico di Azure nel gruppo di risorse. Nuovo servizio di bilanciamento del carico hello è granulare sufficiente tooonly si applicano le macchine virtuali toospecific se necessario. Hello Azure carico di lavoro di regole NAT di bilanciamento del carico insieme tooprovide regole ACL gruppo di sicurezza rete maggiore flessibilità e controllo rispetto a quello ottenibile utilizzando gli endpoint di servizio Cloud è stato. Per ulteriori informazioni, vedere hello [Panoramica del servizio di bilanciamento di carico](../articles/load-balancer/load-balancer-overview.md).

## <a name="network-security-group-acl-rules"></a>Regole ACL dei gruppi di sicurezza di rete
Le regole ACL permettono di definire il traffico consentito in ingresso e in uscita dalla VM in base a porte, intervalli di porte o protocolli specifici. Le regole vengono assegnate le macchine virtuali tooindividual o tooa subnet. Hello schermata seguente è riportato un esempio di regole ACL per un server Web comuni:

![Elenco di regole ACL di un gruppo di sicurezza di rete](./media/virtual-machines-common-endpoints-in-resource-manager/example-acl-rules.png)

Regole ACL vengono applicate in base a una metrica priorità che si specifica - valore hello hello, priorità hello hello. Ogni gruppo di sicurezza di rete con valore predefinito di tre regole che vengono progettati flusso hello toohandle del traffico di rete Azure, con un'esplicita `DenyAllInbound` come regola finale hello. Dato un toonot per priorità bassa regole ACL predefinito sono interferire con le regole create.

## <a name="assigning-network-security-groups"></a>Assegnazione dei gruppi di sicurezza di rete
Assegnare una subnet tooa il gruppo di sicurezza di rete o un'interfaccia di rete. Questo approccio consente toobe granularità in base alle esigenze quando è applicato l'ACL regole tooonly una macchina virtuale specifica, o verificare un set comune di ACL regole vengono applicate tooall parte delle macchine virtuali di una subnet:

![Applicare NSGs toonetwork interfacce o subnet](./media/virtual-machines-common-endpoints-in-resource-manager/apply-nsg-to-resources.png)

comportamento di Hello di hello il gruppo di sicurezza di rete non variano a seconda assegnazione subnet tooa o un'interfaccia di rete. Uno scenario di distribuzione comune è hello che Network Security Group assegnato conformità di tooensure tooa subnet di tutte le macchine virtuali collegati toothat subnet. Per ulteriori informazioni, vedere [l'applicazione di sicurezza di rete gruppi tooresources](../articles/virtual-network/virtual-networks-nsg.md#associating-nsgs).

## <a name="default-behavior-of-network-security-groups"></a>Comportamento predefinito dei gruppi di sicurezza di rete
A seconda di come e quando si crea il gruppo di sicurezza di rete, possono creare regole predefinite per l'accesso RDP toopermit macchine virtuali di Windows sulla porta TCP 3389. Le regole predefinite per le macchine virtuali Linux consentono l'accesso SSH sulla porta TCP 22. Queste regole ACL automatica vengono create in hello seguenti condizioni:

* Se si crea una macchina virtuale di Windows tramite il portale di hello e accetta hello predefinito azione toocreate un gruppo di sicurezza di rete, viene creata una ACL regola tooallow la porta TCP 3389 (RDP).
* Se si crea una VM Linux tramite il portale di hello e accetta hello predefinito azione toocreate un gruppo di sicurezza di rete, viene creata una ACL regola tooallow la porta TCP 22 (SSH).

In tutte le altre condizioni, queste regole ACL predefinite non vengono create. È possibile connettersi tooyour VM senza creare hello regole ACL appropriate. Queste condizioni sono hello azioni comuni seguenti:

* Creazione di un gruppo di sicurezza di rete tramite il portale di hello come un hello toocreating azione distinta macchina virtuale.
* Creazione di un gruppo di sicurezza di rete a livello di codice con PowerShell, l'interfaccia della riga di comando di Azure, API REST e così via.
* Creazione di una macchina virtuale e l'assegnazione gruppo di sicurezza di rete che non dispone già di hello esistente tooan appropriati regola ACL definita.

In hello tutti i casi precedenti, è necessario toocreate le regole ACL per le connessioni di gestione remota appropriata hello tooallow macchina virtuale.

## <a name="default-behavior-of-a-vm-without-a-network-security-group"></a>Comportamento predefinito di una VM senza un gruppo di sicurezza di rete
È possibile creare una VM senza creare un gruppo di sicurezza di rete. In questi casi, è possibile connettersi tooyour VM utilizzando il protocollo RDP o SSH senza creare tutte le regole ACL. Analogamente, se è stato installato un servizio Web sulla porta 80, tale servizio è automaticamente accessibile in remoto. Hello VM siano tutte le porte aperte.

> [!NOTE]
> È comunque necessario toohave un tooa di indirizzo IP di pubblico VM affinché tutte le connessioni remote. Non dispone di un gruppo di sicurezza di rete per l'interfaccia di rete o subnet hello non espone il traffico esterno hello VM tooany. azione predefinita di Hello durante la creazione di una macchina virtuale tramite il portale di hello è toocreate un nuovo indirizzo IP pubblico. In tutte le altre forme di creazione di una VM, come PowerShell, l'interfaccia della riga di comando di Azure o un modello di Resource Manager, non viene creato automaticamente un IP pubblico se non esplicitamente richiesto. azione predefinita Hello tramite il portale di hello è inoltre toocreate un gruppo di sicurezza di rete. Con questa azione predefinita non si dovrebbe quindi verificare la situazione di una VM esposta senza filtri di rete.

## <a name="understanding-load-balancers-and-nat-rules"></a>Informazioni su servizi di bilanciamento del carico e regole NAT
Nel modello di distribuzione classica hello, è possibile creare endpoint effettuate inoltro alla porta. Quando si crea una macchina virtuale nel modello di distribuzione classica hello, verranno create automaticamente regole ACL per RDP o SSH. Queste regole non espone la porta TCP 3389 o la porta TCP 22 rispettivamente toohello all'esterno di world. Al contrario, una porta TCP di alto valore viene esposto che esegue il mapping di porta interna di toohello appropriato. È inoltre possibile creare proprie regole ACL in modo simile, ad esempio espongono un server Web su TCP porta 4280 toohello all'esterno di world. È possibile visualizzare queste regole ACL e i mapping delle porte nella seguente schermata dal portale di hello Classic hello:

![Port forwarding con endpoint del modello di distribuzione classica](./media/virtual-machines-common-endpoints-in-resource-manager/classic-endpoints-port-forwarding.png)

Con i gruppi di sicurezza di rete, la funzione di port forwarding è gestita da un servizio di bilanciamento del carico. Per altre informazioni, vedere la [panoramica dei servizi di bilanciamento del carico in Azure](../articles/load-balancer/load-balancer-overview.md). Hello esempio seguente viene illustrato un servizio di bilanciamento del carico con un NAT regola tooperform inoltro alla porta TCP porta 4222 toohello interno la porta TCP 22 una macchina virtuale:

![Regole NAT del servizio di bilanciamento del carico per il port forwarding](./media/virtual-machines-common-endpoints-in-resource-manager/load-balancer-nat-rules.png)

> [!NOTE]
> Quando si implementa un servizio di bilanciamento del carico, in genere non si assegnano hello macchina virtuale un indirizzo IP pubblico. Servizio di bilanciamento del carico hello dispone invece di un tooit di indirizzo IP pubblico. È comunque necessario toocreate il gruppo di sicurezza di rete e ACL regole toodefine hello flusso del traffico da e verso la macchina virtuale. Hello regole NAT di bilanciamento del carico sono semplicemente toodefine quali porte siano consentiti attraverso bilanciamento del carico hello e come ottenere distribuite su hello back-end le macchine virtuali. Di conseguenza, è necessario toocreate una regola NAT per il traffico tooflow tramite bilanciamento del carico hello. hello tooreach di traffico hello tooallow macchina virtuale, creare una regola ACL di gruppo di sicurezza rete.
