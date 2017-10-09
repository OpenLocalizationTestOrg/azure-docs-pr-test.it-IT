
Se il problema di Azure non viene risolto in questo articolo, visitare hello [forum di Azure su MSDN e l'Overflow dello Stack](https://azure.microsoft.com/support/forums/). È possibile registrare il problema in questi forum o too@AzureSupport su Twitter. Inoltre, è possibile inviare una richiesta di supporto tecnico di Azure selezionando **ottenere supporto** su hello [supporto tecnico di Azure](https://azure.microsoft.com/support/options/) sito.

## <a name="general-troubleshooting-steps"></a>Passaggi per la risoluzione dei problemi generali
### <a name="troubleshoot-common-allocation-failures-in-hello-classic-deployment-model"></a>Risolvere i problemi comuni errori di allocazione nel modello di distribuzione classica hello
Questi passaggi possono facilitare la risoluzione di molti errori di allocazione nelle macchine virtuali:

* Ridimensionare hello VM tooa diverse dimensioni delle macchine Virtuali.<br>
    Fare clic su **Esplora tutto** > **Macchine virtuali (versione classica)** > macchina virtuale > **Impostazioni** > **Dimensioni**. Per informazioni dettagliate, vedere [ridimensionare una macchina virtuale hello](https://msdn.microsoft.com/library/dn168976.aspx).
* Eliminare tutte le macchine virtuali dal servizio cloud hello e ricreare le macchine virtuali.<br>
    Fare clic su **Esplora tutto** > **Macchine virtuali (versione classica)** > macchina virtuale > **Elimina**. Fare quindi clic su **Nuovo** > **Calcolo** > [immagine macchina virtuale].

### <a name="troubleshoot-common-allocation-failures-in-hello-azure-resource-manager-deployment-model"></a>Risolvere i problemi comuni errori di allocazione nel modello di distribuzione Azure Resource Manager hello
Questi passaggi possono facilitare la risoluzione di molti errori di allocazione nelle macchine virtuali:

* Arresta (dealloca) tutte le macchine virtuali in hello stesso disponibilità impostare, quindi riavviare ognuna di esse.<br>
    toostop: fare clic su **gruppi di risorse** > gruppo di risorse > **risorse** > set di disponibilità > **macchine virtuali** > la macchina virtuale >  **Arrestare**.
  
    Dopo l'arresto di tutte le macchine virtuali, selezionare hello prima macchina virtuale e fare clic su **avviare**.

## <a name="background-information"></a>Informazioni generali
### <a name="how-allocation-works"></a>Come funziona l'allocazione
server Hello in Data Center di Azure vengono partizionati in cluster. In genere, viene eseguito un tentativo di una richiesta di allocazione in più cluster, ma è possibile che alcuni vincoli dalla richiesta di allocazione hello forzare la richiesta di hello piattaforma Azure tooattempt hello in un solo cluster. In questo articolo, si farà riferimento toothis come "aggiunto tooa cluster". Il diagramma 1 di viene illustrato il caso di hello di un'allocazione normale che viene eseguito un tentativo di più cluster. Diagramma 2 viene illustrato il caso di hello di un'allocazione che è stato aggiunto tooCluster 2 perché è in cui è ospitato hello set di disponibilità o CS_1 servizio Cloud esistente.
![Diagramma di allocazione](./media/virtual-machines-common-allocation-failure/Allocation1.png)

### <a name="why-allocation-failures-happen"></a>Perché si verificano gli errori di allocazione
Quando una richiesta di allocazione è bloccata tooa cluster, è una maggiore probabilità di esito positivo toofind liberare le risorse in quanto il pool di risorse disponibili hello è inferiore. Inoltre, se la richiesta di allocazione è bloccata tooa cluster, ma il tipo di hello della risorsa richiesta non è supportato da tale cluster, la richiesta avrà esito negativo anche se il cluster hello è liberare le risorse. Diagramma 3 riportato di seguito viene illustrato case hello in cui un'allocazione aggiunta non riesce perché non dispone di liberare le risorse cluster solo candidato hello. Figura 4 viene illustrata case hello in cui un'allocazione aggiunta non riesce perché non supporta i cluster candidato solo hello hello richiesto dimensioni delle macchine Virtuali, anche se sono presenti cluster hello liberare risorse.

![Errore di allocazione bloccata](./media/virtual-machines-common-allocation-failure/Allocation2.png)

## <a name="detailed-troubleshoot-steps-specific-allocation-failure-scenarios-in-hello-classic-deployment-model"></a>Dettagliate risolvere scenari di errore specifici di allocazioni passaggi nel modello di distribuzione classica hello
Di seguito sono comuni scenari di allocazione che comportano un toobe di richiesta di allocazione bloccato. Verrà esaminato ogni scenario più avanti in questo articolo.

* Ridimensionare una macchina virtuale o aggiungere le macchine virtuali o il servizio cloud esistente di ruolo istanze tooan
* Riavviare VM arrestate (deallocate) parzialmente
* Riavviare VM arrestate (deallocate) completamente
* Distribuzioni di gestione temporanea o di produzione (solo Platform-as-a-Service)
* Gruppo di affinità (prossimità di VM o servizio)
* Rete virtuale basata su gruppi di affinità

Quando si riceve un errore di allocazione, vedere se uno degli scenari di hello descritti tooyour errore di applicazione. Utilizzare l'errore di allocazione hello restituito da uno scenario di corrispondente hello piattaforma Azure tooidentify hello. Se la richiesta è bloccata, rimuovere alcuni hello blocco vincoli tooopen i cluster toomore richiesta, aumentando il possibilità di successo di allocazione di hello.

In generale, purché hello errore non indica "hello" necessaria manutenzione dimensioni della macchina virtuale non sono supportata", è possibile sempre riprovare in un secondo momento, come risorse sufficienti potrebbero essere stato liberato in hello cluster tooaccommodate la richiesta. Se il problema di hello che hello richiesto dimensioni della macchina virtuale non sono supportata, provare a una dimensione di macchina virtuale diversa. In caso contrario, hello è solo hello tooremove il blocco di vincolo.

Due scenari di errore comuni sono gruppi di tooaffinity correlati. In hello precedente, un gruppo di affinità utilizzato tooprovide prossimità tooVMs/istanze servizio, o sono utilizzati tooenable hello creazione di una rete virtuale. Con l'introduzione di hello di reti virtuali regionali, gruppi di affinità non sono più necessari toocreate una rete virtuale. Con la riduzione della latenza di rete nell'infrastruttura di Azure hello, gruppi di affinità di hello raccomandazione toouse per prossimità/servizio della macchina virtuale è stata modificata.

Diagramma 5 di seguito viene presentato tassonomia hello degli scenari di allocazione hello (bloccato).
![Tassonomia di allocazione bloccata](./media/virtual-machines-common-allocation-failure/Allocation3.png)

> [!NOTE]
> Errore di Hello elencato in ogni scenario di allocazione è una forma abbreviata. Fare riferimento toohello [ricerca della stringa di errore](#Error string lookup) per le stringhe di errore dettagliato.
> 
> 

## <a name="allocation-scenario-resize-a-vm-or-add-vms-or-role-instances-tooan-existing-cloud-service"></a>Scenario di allocazione: ridimensionare una macchina virtuale o aggiungere istanze del servizio cloud esistente tooan ruolo o macchine virtuali
**Errore**

Upgrade_VMSizeNotSupported o GeneralError

**Causa del blocco su un cluster**

Richiesta tooresize una macchina virtuale o aggiungere una macchina virtuale o un servizio ruolo di istanza tooan esistente cloud ha toobe tentata al cluster originale hello che ospita il servizio cloud esistente di hello. Consente la creazione di un nuovo servizio cloud hello piattaforma Azure toofind un altro cluster che è liberare le risorse o supporta le dimensioni della macchina virtuale hello richiesto.

**Soluzione alternativa**

Se l'errore hello è Upgrade_VMSizeNotSupported *, provare a una dimensione di macchina virtuale diversa. Se l'utilizzo di diverse dimensioni macchina virtuale non è un'opzione, ma se è accettabile toouse un diverso indirizzo IP virtuale (VIP), creare un nuovo toohost servizio cloud hello nuova macchina virtuale e aggiungere hello nuovo cloud toohello internazionali rete virtuale del servizio in cui hello macchine virtuali esistenti sono in esecuzione. Se il servizio cloud esistente non utilizza una rete virtuale regionale, è possibile comunque creare una nuova rete virtuale per il servizio cloud nuovo hello e quindi connettere il [rete virtuale toohello nuova rete virtuale esistente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Altre informazioni sulle [reti virtuali a livello di area](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Se l'errore hello è GeneralError *, è probabile che il tipo di hello di risorsa (ad esempio una determinata dimensione di macchina virtuale) è supportato dal cluster hello, ma cluster hello privo di liberare le risorse in un momento hello. Toohello simile di sopra di uno scenario, aggiungere risorse di calcolo hello desiderata tramite la creazione di un nuovo servizio cloud (si noti che nuovo servizio cloud di hello è toouse un VIP diverso) e utilizzare tooconnect una rete virtuale regionale i servizi cloud.

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Scenario di allocazione: riavviare VM arrestate (deallocate) parzialmente
**Errore**

GeneralError*

**Causa del blocco su un cluster**

La deallocazione parziale significa che una o più macchine virtuali in un servizio cloud sono state arrestate (deallocate), ma non tutte. Quando si arresta (dealloca) una macchina virtuale, hello associata le risorse vengono rilasciate. Il riavvio della VM arrestata (deallocata) è quindi una nuova richiesta di allocazione. Riavvio delle macchine virtuali in un servizio cloud parzialmente deallocata è equivalente tooadding servizio cloud di macchine virtuali tooan esistente. richiesta di allocazione Hello è toobe tentata al cluster originale hello che ospita il servizio cloud esistente di hello. Consente la creazione di un servizio cloud diverso hello piattaforma Azure toofind un altro cluster che è una risorsa gratuita o supporta le dimensioni della macchina virtuale hello richiesto.

**Soluzione alternativa**

Se è accettabile un diverso indirizzo VIP, hello di eliminazione toouse arrestata (deallocate) le macchine virtuali (ma mantenere hello associato dischi) e aggiunta hello macchine virtuali tramite un servizio cloud diverso. Utilizzare una rete virtuale regionale di tooconnect i servizi cloud:

* Se il servizio cloud esistente Usa una rete virtuale regionale, aggiungere semplicemente hello nuovo cloud servizio toohello stessa rete virtuale.
* Se il servizio cloud esistente non utilizza una rete virtuale regionale, creare una nuova rete virtuale per il nuovo servizio cloud di hello e quindi [connettersi la rete virtuale toohello nuova rete virtuale esistente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Altre informazioni sulle [reti virtuali a livello di area](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

## <a name="allocation-scenario-restart-fully-stopped-deallocated-vms"></a>Scenario di allocazione: riavviare VM arrestate (deallocate) completamente
**Errore**

GeneralError*

**Causa del blocco su un cluster**

La deallocazione completa significa che sono state arrestate (deallocate) tutte le VM da un servizio cloud. queste macchine virtuali hanno toobe tentata al cluster originale hello che ospita il servizio cloud hello toorestart delle richieste di allocazione Hello. Consente la creazione di un nuovo servizio cloud hello piattaforma Azure toofind un altro cluster che è liberare le risorse o supporta le dimensioni della macchina virtuale hello richiesto.

**Soluzione alternativa**

Se è accettabile toouse un VIP diverso, hello delete originale arrestata (deallocate) le macchine virtuali (ma i dischi associato hello keep) e di eliminare il servizio cloud corrispondente hello (calcolo di hello associato alle risorse già rilasciate quando è stato arrestato (deallocato) Hello macchine virtuali). Creare un nuovo hello tooadd di servizio cloud macchine virtuali nuovamente.

## <a name="allocation-scenario-stagingproduction-deployments-platform-as-a-service-only"></a>Scenario di allocazione: distribuzioni di gestione temporanea/produzione (solo Platform-as-a-Service)
**Errore**

New_General* o New_VMSizeNotSupported*

**Causa del blocco su un cluster**

distribuzione e la distribuzione di produzione hello di un servizio cloud di gestione temporanea Hello è ospitato in hello dello stesso cluster. Quando si aggiunge una seconda distribuzione hello, richiesta di allocazione corrispondente hello verrà tentata in hello dello stesso cluster che ospita hello prima distribuzione.

**Soluzione alternativa**

Eliminare prima distribuzione hello e il servizio cloud originale hello e ridistribuire il servizio di cloud hello. Questa azione potrebbe rimanere prima distribuzione hello in un cluster che dispone di entrambe le distribuzioni toofit sufficiente liberare le risorse o in un cluster che supporta dimensioni di macchina virtuale hello richiesto.

## <a name="allocation-scenario-affinity-group-vmservice-proximity"></a>Scenario di allocazione: gruppo di affinità (prossimità di VM o servizi)
**Errore**

New_General* o New_VMSizeNotSupported*

**Causa del blocco su un cluster**

Qualsiasi risorsa di calcolo è il gruppo di affinità assegnato tooan legati tooone cluster. Nuove richieste di risorse di calcolo in tale gruppo di affinità vengono tentate in hello stesso cluster ospitate risorse esistenti hello. È true se le nuove risorse hello vengono create tramite un nuovo servizio cloud o un servizio cloud esistente.

**Soluzione alternativa**

Se un gruppo di affinità non è necessario, non usare un gruppo di affinità o raggruppare le risorse di calcolo in più gruppi di affinità.

## <a name="allocation-scenario-affinity-group-based-virtual-network"></a>Scenario di allocazione: rete virtuale basata su gruppi di affinità
**Errore**

New_General* o New_VMSizeNotSupported*

**Causa del blocco su un cluster**

Prima dell'introduzione delle reti virtuali regionali, era necessario tooassociate una rete virtuale con un gruppo di affinità. Di conseguenza, le risorse di calcolo inserite in un gruppo di affinità sono legate da hello stessi vincoli, come descritto in hello "scenario di allocazione: gruppo di affinità (prossimità/servizio della macchina virtuale)" sezione precedente. risorse di calcolo Hello sono legati tooone cluster.

**Soluzione alternativa**

Se non è necessario un gruppo di affinità, creare una nuova rete virtuale regionale per hello nuove risorse per aggiungere, quindi [connettersi la rete virtuale toohello nuova rete virtuale esistente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Altre informazioni sulle [reti virtuali a livello di area](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

In alternativa, è possibile [eseguire la migrazione della rete virtuale regionale rete virtuale basato su gruppo di affinità tooa](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), quindi aggiungere nuovamente le risorse di hello desiderato.

## <a name="detailed-troubleshooting-steps-specific-allocation-failure-scenarios-in-hello-azure-resource-manager-deployment-model"></a>Risoluzione dei problemi di scenari di errore specifici di allocazioni di passaggi nel modello di distribuzione Azure Resource Manager hello dettagliata
Di seguito sono comuni scenari di allocazione che comportano un toobe di richiesta di allocazione bloccato. Verrà esaminato ogni scenario più avanti in questo articolo.

* Ridimensionare una macchina virtuale o aggiungere le macchine virtuali o il servizio cloud esistente di ruolo istanze tooan
* Riavviare VM arrestate (deallocate) parzialmente
* Riavviare VM arrestate (deallocate) completamente

Quando si riceve un errore di allocazione, vedere se uno degli scenari di hello descritti tooyour errore di applicazione. Utilizzare l'errore di allocazione hello restituito da uno scenario di corrispondente hello piattaforma Azure tooidentify hello. Se la richiesta è di tipo cluster esistente tooan bloccati, rimuovere alcuni hello blocco vincoli tooopen i cluster toomore richiesta, aumentando il possibilità di successo di allocazione di hello.

In generale, purché hello errore non indica "hello" necessaria manutenzione dimensioni della macchina virtuale non sono supportata", è possibile sempre riprovare in un secondo momento, come risorse sufficienti potrebbero essere stato liberato in hello cluster tooaccommodate la richiesta. Se il problema di hello che hello richiesto dimensioni della macchina virtuale non sono supportata, vedere di seguito per soluzioni alternative.

## <a name="allocation-scenario-resize-a-vm-or-add-vms-tooan-existing-availability-set"></a>Scenario di allocazione: ridimensionare una macchina virtuale o aggiungere le macchine virtuali tooan set di disponibilità esistente
**Errore**

Upgrade_VMSizeNotSupported* o GeneralError*

**Causa del blocco su un cluster**

Richiesta tooresize una macchina virtuale o aggiungere tooan una macchina virtuale esistente di set di disponibilità ha toobe tentata al cluster originale hello che ospita il set di disponibilità esistente hello. Creazione di un nuovo set di disponibilità consente hello piattaforma Azure toofind un altro cluster che è liberare le risorse o supporta le dimensioni della macchina virtuale hello richiesto.

**Soluzione alternativa**

Se l'errore hello è Upgrade_VMSizeNotSupported *, provare a una dimensione di macchina virtuale diversa. Se l'utilizzo di diverse dimensioni macchina virtuale non è un'opzione, è possibile arrestare tutte le macchine virtuali nel set di disponibilità hello. È possibile quindi lo si desidera modificare le dimensioni di macchina virtuale hello allocherà cluster tooa della macchina virtuale hello che supporta hello hello dimensioni della macchina virtuale.

Se l'errore hello è GeneralError *, è probabile che il tipo di hello di risorsa (ad esempio una determinata dimensione di macchina virtuale) è supportato dal cluster hello, ma cluster hello privo di liberare le risorse in un momento hello. Se hello VM può essere parte di un set di disponibilità diverso, è possibile creare una nuova macchina virtuale in un set di disponibilità diverso (in hello stessa regione). Questa nuova macchina virtuale può essere aggiunti toohello stessa rete virtuale.  

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Scenario di allocazione: riavviare VM arrestate (deallocate) parzialmente
**Errore**

GeneralError*

**Causa del blocco su un cluster**

La deallocazione parziale significa che una o più VM in un set di disponibilità sono state arrestate (deallocate), ma non tutte. Quando si arresta (dealloca) una macchina virtuale, hello associata le risorse vengono rilasciate. Il riavvio della VM arrestata (deallocata) è quindi una nuova richiesta di allocazione. Riavvio delle macchine virtuali in un set di disponibilità parzialmente deallocata è equivalente tooadding gruppo di disponibilità di macchine virtuali tooan impostato. richiesta di allocazione Hello è toobe tentata al cluster originale hello che ospita il set di disponibilità esistente hello.

**Soluzione alternativa**

Arrestare tutte le macchine virtuali nel set prima di riavviare hello prima di disponibilità di hello. Questo garantisce che venga eseguito un nuovo tentativo di allocazione e che si possa selezionare un nuovo cluster con capacità disponibile.

## <a name="allocation-scenario-restart-fully-stopped-deallocated"></a>Scenario di allocazione: riavviare in caso di arresto (deallocazione) completo
**Errore**

GeneralError*

**Causa del blocco su un cluster**

La deallocazione completa significa che sono state arrestate (deallocate) tutte le VM in un set di disponibilità. richiesta di allocazione Hello toorestart queste macchine virtuali saranno destinati a tutti i cluster che supportano hello dimensioni desiderate.

**Soluzione alternativa**

Selezionare un nuovo tooallocate dimensioni macchina virtuale. Se non funziona, riprovare in seguito.

## <a name="error-string-lookup"></a>Ricerca della stringa di errore
**New_VMSizeNotSupported***

"hello VM dimensioni (o combinazione di dimensioni delle macchine Virtuali) richieste da questa distribuzione non è possibile eseguirne il provisioning a causa di vincoli richiesta toodeployment. Se possibile, provare a rilasciare vincoli quali associazioni a reti virtuali, distribuzione del servizio ospitato tooa con alcun'altra distribuzione in essa contenuti e la distribuzione di tooa affinità diverso o gruppo con alcun gruppo di affinità oppure provare a area diversa tooa. "

**New_General***

"L'allocazione non riuscita. non è possibile toosatisfy vincoli nella richiesta. nuova distribuzione del servizio richiesto Hello è il gruppo di affinità tooan associati, o faccia riferimento a una rete virtuale è una distribuzione esistente in questo servizio ospitato. Una di queste condizioni vincola hello nuova distribuzione toospecific Azure le risorse. . Riprovare più tardi o provare a ridurre le dimensioni VM hello o numero di istanze del ruolo. In alternativa, se possibile, rimuovere i vincoli sopra hello o provare a distribuire area diversa tooa."

**Upgrade_VMSizeNotSupported***

"Distribuzione hello tooupgrade non è possibile. Hello richiesto XXX dimensioni della macchina virtuale potrebbero non essere disponibile nelle risorse hello che supporta la distribuzione esistente di hello. Riprovare più tardi, provare con una dimensione della macchina virtuale diversa o con un numero minore di istanze del ruolo oppure creare una distribuzione in un servizio ospitato vuoto con un nuovo gruppo di affinità o senza associazione a un gruppo di affinità".

**GeneralError***

"server hello verificato un errore interno. Ritentare la richiesta hello." O "Failed tooproduce un'allocazione per il servizio hello".

