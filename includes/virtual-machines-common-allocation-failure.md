
Se il problema di Azure non viene risolto in questo articolo, visitare il [forum di Azure su MSDN e Overflow dello Stack](https://azure.microsoft.com/support/forums/). È possibile pubblicare il problema in questi forum o in @AzureSupport su Twitter. È anche possibile inviare una richiesta di supporto tecnico di Azure selezionando **Ottieni supporto** nel sito del [supporto tecnico di Azure](https://azure.microsoft.com/support/options/).

## <a name="general-troubleshooting-steps"></a>Passaggi per la risoluzione dei problemi generali
### <a name="troubleshoot-common-allocation-failures-in-the-classic-deployment-model"></a>Risolvere i problemi relativi a errori comuni di allocazione nel modello di distribuzione classico
Questi passaggi possono facilitare la risoluzione di molti errori di allocazione nelle macchine virtuali:

* Ridimensionare la macchina virtuale con una dimensione diversa della macchina virtuale.<br>
    Fare clic su **Sfoglia tutto** > **macchine virtuali (classico)** > la macchina virtuale > **impostazioni** > **dimensioni**. Per i passaggi dettagliati, vedere l'articolo relativo al [Ridimensionamento della macchina virtuale](https://msdn.microsoft.com/library/dn168976.aspx).
* Eliminare tutte le VM dal servizio cloud e ricrearle.<br>
    Fare clic su **Sfoglia tutto** > **macchine virtuali (classico)** > la macchina virtuale > **eliminare**. Fare quindi clic su **Nuovo** > **Calcolo** > [immagine macchina virtuale].

### <a name="troubleshoot-common-allocation-failures-in-the-azure-resource-manager-deployment-model"></a>Risolvere i problemi relativi a errori comuni di allocazione nel modello di distribuzione di Gestione risorse di Azure
Questi passaggi possono facilitare la risoluzione di molti errori di allocazione nelle macchine virtuali:

* Arrestare (deallocare) tutte le VM nello stesso set di disponibilità, quindi riavviarle tutte.<br>
    Per arrestare: fare clic su **gruppi di risorse** > gruppo di risorse > **risorse** > set di disponibilità > **macchine virtuali** > la macchina virtuale >  **Arrestare**.
  
    Dopo l'arresto di tutte le VM, selezionare la prima e fare clic su **Avvia**.

## <a name="background-information"></a>Informazioni generali
### <a name="how-allocation-works"></a>Come funziona l'allocazione
I server nei data center di Azure sono partizionati in cluster. In genere, viene eseguita una richiesta di allocazione in più cluster, ma è possibile che determinati vincoli nella richiesta di allocazione impongano alla piattaforma Azure di eseguire la richiesta in un solo cluster. In questo articolo, si fa riferimento a questa operazione con l'espressione "bloccata su un cluster". Il diagramma 1 riportato di seguito illustra il caso di un'allocazione normale tentata in più cluster. Il diagramma 2 illustra il caso di un'allocazione bloccata sul cluster 2 perché è quello che ospita il servizio cloud CS_1 o il set di disponibilità esistente.
![Diagramma di allocazione](./media/virtual-machines-common-allocation-failure/Allocation1.png)

### <a name="why-allocation-failures-happen"></a>Perché si verificano gli errori di allocazione
Quando una richiesta di allocazione è bloccata su un cluster, la probabilità di non riuscire a trovare risorse disponibili è più alta, perché il pool di risorse disponibili è più ridotto. Inoltre, se la richiesta di allocazione è bloccata su un cluster, ma il tipo di risorsa richiesto non è supportato da quel cluster, la richiesta non viene eseguita correttamente anche se nel cluster ci sono risorse disponibili. Il diagramma 3 seguente illustra un'allocazione bloccata non riuscita perché nel solo cluster candidato non ci sono risorse disponibili. Il diagramma 4 illustra un'allocazione bloccata non riuscita perché il solo cluster candidato non supporta le dimensioni della VM richieste, anche se nel cluster ci sono risorse disponibili.

![Errore di allocazione bloccata](./media/virtual-machines-common-allocation-failure/Allocation2.png)

## <a name="detailed-troubleshoot-steps-specific-allocation-failure-scenarios-in-the-classic-deployment-model"></a>Risolvere i problemi relativi a scenari di errori di allocazione specifici nel modello di distribuzione classico
Ecco gli scenari di allocazione comuni che causano una richiesta di allocazione da bloccare. Verrà esaminato ogni scenario più avanti in questo articolo.

* Ridimensionare una VM o aggiungere VM o istanze dei ruoli a un servizio cloud esistente
* Riavviare VM arrestate (deallocate) parzialmente
* Riavviare VM arrestate (deallocate) completamente
* Distribuzioni di gestione temporanea o di produzione (solo Platform-as-a-Service)
* Gruppo di affinità (prossimità di VM o servizio)
* Rete virtuale basata su gruppi di affinità

Quando si riceve un errore di allocazione, verificare se uno degli scenari descritti è pertinente con questo errore. Usare l'errore di allocazione restituito dalla piattaforma Azure per identificare lo scenario corrispondente. Se la richiesta è bloccata, rimuovere alcuni dei vincoli di blocco per aprire la richiesta a più cluster, aumentando quindi la possibilità di eseguire l'allocazione correttamente.

In generale, finché l'errore non indica che le dimensioni della VM richieste non sono supportate, è sempre possibile riprovare in un secondo momento perché nel cluster potrebbero liberarsi risorse sufficienti per soddisfare la richiesta. Se il problema è che la dimensione della VM richiesta non è supportata, provare con una dimensione diversa di VM. In caso contrario, l'unica opzione consiste nel rimuovere il vincolo di blocco.

Due scenari di errore comuni sono correlati ai gruppi di affinità. In passato, il gruppo di affinità veniva usato per fornire la prossimità alle istanze di VM o servizi o per abilitare la creazione della rete virtuale. Con l'introduzione delle reti virtuali dell'area, i gruppi di affinità non sono più necessari per creare una rete virtuale. Con la riduzione della latenza di rete nell'infrastruttura di Azure, l'indicazione che riguarda l'uso dei gruppi di affinità per la prossimità di VM o servizi è stata modificata.

Il diagramma 5 seguente illustra la tassonomia degli scenari di allocazione (bloccata).
![Tassonomia di allocazione bloccata](./media/virtual-machines-common-allocation-failure/Allocation3.png)

> [!NOTE]
> L'errore indicato in ogni scenario di allocazione è in forma breve. Per le stringhe di errore dettagliate, vedere [Ricerca della stringa di errore](#Error string lookup).
> 
> 

## <a name="allocation-scenario-resize-a-vm-or-add-vms-or-role-instances-to-an-existing-cloud-service"></a>Scenario di allocazione: ridimensionare una VM o aggiungere altre VM o istanze dei ruoli a un servizio cloud esistente
**Errore**

Upgrade_VMSizeNotSupported o GeneralError

**Causa del blocco su un cluster**

La richiesta di ridimensionamento di una VM o di aggiunta di una VM o di un'istanza del ruolo a un servizio cloud esistente deve essere eseguita nel cluster originale che ospita il servizio cloud esistente. La creazione di un nuovo servizio cloud consente alla piattaforma Azure di trovare un altro cluster con risorse disponibili o che supporti le dimensioni della VM richieste.

**Soluzione alternativa**

Se l'errore è Upgrade_VMSizeNotSupported*, provare con dimensioni della VM diverse. Se l'uso di dimensioni della VM diverse non è possibile, ma è accettabile usare un indirizzo IP virtuale (indirizzo VIP) diverso, creare un nuovo servizio cloud per ospitare la nuova VM e aggiungere il nuovo servizio cloud alla rete virtuale dell'area in cui sono in esecuzione le VM esistenti. Se il servizio cloud esistente non usa una rete virtuale dell'area, è comunque possibile creare una nuova rete virtuale per il nuovo servizio cloud, quindi connettere la [rete virtuale esistente a quella nuova](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Altre informazioni sulle [reti virtuali a livello di area](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Se l'errore è GeneralError, è probabile che il tipo di risorsa (ad esempio, le dimensioni specifiche della VM) sia supportato dal cluster, che al momento non dispone di risorse disponibili. Analogamente allo scenario riportato sopra, aggiungere la risorsa di calcolo desiderata tramite la creazione di un nuovo servizio cloud (notare che il nuovo servizio cloud deve usare un indirizzo VIP diverso) e usare una rete virtuale dell'area per connettere i servizi cloud.

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Scenario di allocazione: riavviare VM arrestate (deallocate) parzialmente
**Errore**

GeneralError*

**Causa del blocco su un cluster**

La deallocazione parziale significa che una o più macchine virtuali in un servizio cloud sono state arrestate (deallocate), ma non tutte. Quando si arresta (viene deallocata) una VM, vengono rilasciate le risorse associate. Il riavvio della VM arrestata (deallocata) è quindi una nuova richiesta di allocazione. Riavviare le VM in un servizio cloud parzialmente deallocato equivale ad aggiungere VM a un servizio cloud esistente. La richiesta di allocazione deve essere eseguita nel cluster originale che ospita il servizio cloud esistente. La creazione di un servizio cloud diverso consente alla piattaforma Azure di trovare un altro cluster con risorse disponibili o che supporti le dimensioni della VM richieste.

**Soluzione alternativa**

Se è accettabile usare un indirizzo VIP diverso, eliminare le VM arrestate (deallocate), mantenendo però i dischi associati, quindi riaggiungere le VM tramite un servizio cloud diverso. Usare una rete virtuale dell'area per connettere i servizi cloud:

* Se il servizio cloud esistente usa una rete virtuale dell'area, è sufficiente aggiungere il nuovo servizio cloud alla stessa rete virtuale.
* Se il servizio cloud esistente non usa una rete virtuale dell'area, creare una nuova rete virtuale per il nuovo servizio cloud, quindi connettere la [rete virtuale esistente a quella nuova](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Altre informazioni sulle [reti virtuali a livello di area](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

## <a name="allocation-scenario-restart-fully-stopped-deallocated-vms"></a>Scenario di allocazione: riavviare VM arrestate (deallocate) completamente
**Errore**

GeneralError*

**Causa del blocco su un cluster**

La deallocazione completa significa che sono state arrestate (deallocate) tutte le VM da un servizio cloud. Le richieste di allocazione per il riavvio di queste VM devono essere eseguite nel cluster originale che ospita il servizio cloud. La creazione di un nuovo servizio cloud consente alla piattaforma Azure di trovare un altro cluster con risorse disponibili o che supporti le dimensioni della VM richieste.

**Soluzione alternativa**

Se è accettabile usare un indirizzo VIP diverso, eliminare le VM arrestate (deallocate) originali, mantenendo però i dischi associati, quindi eliminare il servizio cloud corrispondente. Le risorse di calcolo associate sono già state rilasciate al momento dell'arresto (deallocazione) delle VM. Creare un nuovo servizio cloud per riaggiungere le VM.

## <a name="allocation-scenario-stagingproduction-deployments-platform-as-a-service-only"></a>Scenario di allocazione: distribuzioni di gestione temporanea/produzione (solo Platform-as-a-Service)
**Errore**

New_General * o * New_VMSizeNotSupported

**Causa del blocco su un cluster**

Le distribuzione di gestione temporanea e di produzione di un servizio cloud sono ospitate nello stesso cluster. Quando si aggiunge la seconda distribuzione, la richiesta di allocazione corrispondente verrà eseguita nello stesso cluster che ospita la prima distribuzione.

**Soluzione alternativa**

Eliminare la prima distribuzione e il servizio cloud originale, quindi ridistribuire il servizio cloud. Questa azione potrebbe inserire la prima distribuzione in un cluster con risorse disponibili sufficienti per entrambe le distribuzioni o in un cluster che supporta le dimensioni della VM richieste.

## <a name="allocation-scenario-affinity-group-vmservice-proximity"></a>Scenario di allocazione: gruppo di affinità (prossimità di VM o servizi)
**Errore**

New_General * o * New_VMSizeNotSupported

**Causa del blocco su un cluster**

Qualsiasi risorsa di calcolo assegnata a un gruppo di affinità è associata a un cluster. Le nuove richieste di risorse di calcolo in quel gruppo di affinità vengono eseguite nello stesso cluster in cui sono ospitate le risorse esistenti. Questo vale indipendentemente dal fatto che le nuove risorse vengano create tramite un servizio cloud nuovo o esistente.

**Soluzione alternativa**

Se un gruppo di affinità non è necessario, non usare un gruppo di affinità o raggruppare le risorse di calcolo in più gruppi di affinità.

## <a name="allocation-scenario-affinity-group-based-virtual-network"></a>Scenario di allocazione: rete virtuale basata su gruppi di affinità
**Errore**

New_General * o * New_VMSizeNotSupported

**Causa del blocco su un cluster**

Prima dell'introduzione delle reti virtuali dell'area, era necessario associare una rete virtuale a un gruppo di affinità. Di conseguenza, le risorse di calcolo inserite in un gruppo di affinità sono soggette agli stessi vincoli descritti nella sezione "Scenario di allocazione: gruppo di affinità (prossimità di VM o servizi)" riportata sopra. Le risorse di calcolo sono legate a un cluster.

**Soluzione alternativa**

Se il gruppo di affinità non è necessario, creare una nuova rete virtuale dell'area per le nuove risorse aggiunte, quindi [connettere la rete virtuale esistente a quella nuova](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Altre informazioni sulle [reti virtuali a livello di area](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

In alternativa, è possibile [eseguire la migrazione della rete virtuale basata su gruppi di affinità alla rete virtuale dell'area](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), quindi aggiungere di nuovo le risorse desiderate.

## <a name="detailed-troubleshooting-steps-specific-allocation-failure-scenarios-in-the-azure-resource-manager-deployment-model"></a>Procedura di risoluzione dei problemi dettagliata relativa a scenari con errori di allocazione nel modello di distribuzione Azure Resource Manager
Ecco gli scenari di allocazione comuni che causano una richiesta di allocazione da bloccare. Verrà esaminato ogni scenario più avanti in questo articolo.

* Ridimensionare una VM o aggiungere VM o istanze dei ruoli a un servizio cloud esistente
* Riavviare VM arrestate (deallocate) parzialmente
* Riavviare VM arrestate (deallocate) completamente

Quando si riceve un errore di allocazione, verificare se uno degli scenari descritti è pertinente con questo errore. Usare l'errore di allocazione restituito dalla piattaforma Azure per identificare lo scenario corrispondente. Se la richiesta è bloccata su un cluster esistente, rimuovere alcuni dei vincoli di blocco per aprire la richiesta a più cluster, aumentando quindi la possibilità di eseguire l'allocazione correttamente.

In generale, finché l'errore non indica che le dimensioni della VM richieste non sono supportate, è sempre possibile riprovare in un secondo momento perché nel cluster potrebbero liberarsi risorse sufficienti per soddisfare la richiesta. Se il problema consiste nel fatto che le dimensioni richieste per la VM non sono supportate, vedere di seguito le soluzioni alternative.

## <a name="allocation-scenario-resize-a-vm-or-add-vms-to-an-existing-availability-set"></a>Scenario di allocazione: ridimensionare una VM o aggiungere VM a un set di disponibilità esistente
**Errore**

Upgrade_VMSizeNotSupported * o * GeneralError

**Causa del blocco su un cluster**

La richiesta di ridimensionamento di una VM o di aggiunta di una VM a un set di disponibilità esistente deve essere eseguita nel cluster originale che ospita il set di disponibilità esistente. La creazione di un nuovo set di disponibilità consente alla piattaforma Azure di trovare un altro cluster con risorse disponibili o che supporti le dimensioni della VM richieste.

**Soluzione alternativa**

Se l'errore è Upgrade_VMSizeNotSupported*, provare con dimensioni della VM diverse. Se non è possibile usare dimensioni della VM diverse, arrestare tutte le VM nel set di disponibilità. In questo modo, è possibile modificare le dimensioni della macchina virtuale che alloca la VM a un cluster che supporta le dimensioni della VM desiderate.

Se l'errore è GeneralError, è probabile che il tipo di risorsa (ad esempio, le dimensioni specifiche della VM) sia supportato dal cluster, che al momento non dispone di risorse disponibili. Se la VM può far parte di un set di disponibilità diverso, creare una nuova VM in un altro set di disponibilità nella stessa area. La nuova VM può quindi essere aggiunta alla stessa rete virtuale.  

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Scenario di allocazione: riavviare VM arrestate (deallocate) parzialmente
**Errore**

GeneralError*

**Causa del blocco su un cluster**

La deallocazione parziale significa che una o più VM in un set di disponibilità sono state arrestate (deallocate), ma non tutte. Quando si arresta (viene deallocata) una VM, vengono rilasciate le risorse associate. Il riavvio della VM arrestata (deallocata) è quindi una nuova richiesta di allocazione. Riavviare le VM in un set di disponibilità parzialmente deallocato equivale ad aggiungere VM a un set di disponibilità esistente. La richiesta di allocazione deve essere eseguita nel cluster originale che ospita il set di disponibilità esistente.

**Soluzione alternativa**

Arrestare tutte le VM nel set di disponibilità prima di riavviare la prima. Questo garantisce che venga eseguito un nuovo tentativo di allocazione e che si possa selezionare un nuovo cluster con capacità disponibile.

## <a name="allocation-scenario-restart-fully-stopped-deallocated"></a>Scenario di allocazione: riavviare in caso di arresto (deallocazione) completo
**Errore**

GeneralError*

**Causa del blocco su un cluster**

La deallocazione completa significa che sono state arrestate (deallocate) tutte le VM in un set di disponibilità. La richiesta di allocazione per il riavvio di queste VM viene eseguita in tutti i cluster che supportano le dimensioni desiderate.

**Soluzione alternativa**

Selezionare una nuova dimensione di VM da allocare. Se non funziona, riprovare in seguito.

## <a name="error-string-lookup"></a>Ricerca della stringa di errore
**New_VMSizeNotSupported***

"Impossibile eseguire il provisioning delle dimensioni della macchina virtuale (o della combinazione di dimensioni delle macchine virtuali) richieste da questa distribuzione, a causa di vincoli della richiesta di distribuzione. Se possibile, provare a rilasciare vincoli quali associazioni a reti virtuali, distribuzione a un servizio ospitato che non include alcun'altra distribuzione e a un gruppo di affinità diverso o senza alcun gruppo di affinità oppure provare a distribuire in un'area diversa".

**New_General***

Allocazione non riuscita. Impossibile soddisfare i vincoli nella richiesta. La nuova distribuzione del servizio richiesta è vincolata a un gruppo di affinità, ha come destinazione una rete virtuale o è presente una distribuzione esistente in questo servizio ospitato. Una di queste condizioni vincola la nuova distribuzione a risorse Azure specifiche. Riprovare più tardi o provare a ridurre le dimensioni della macchina virtuale o il numero di istanze del ruolo. In alternativa, è possibile rimuovere i vincoli sopra indicati o tentare di distribuire in un'area diversa".

**Upgrade_VMSizeNotSupported***

"Non è possibile eseguire l'aggiornamento della distribuzione. È possibile che la dimensione della macchina virtuale XXX richiesta non sia disponibile nella distribuzione esistente. Riprovare più tardi, provare con una dimensione della macchina virtuale diversa o con un numero minore di istanze del ruolo oppure creare una distribuzione in un servizio ospitato vuoto con un nuovo gruppo di affinità o senza associazione a un gruppo di affinità".

**GeneralError***

"Errore interno del server. Ritentare la richiesta" o "Non è stato possibile produrre un'allocazione per il servizio".

