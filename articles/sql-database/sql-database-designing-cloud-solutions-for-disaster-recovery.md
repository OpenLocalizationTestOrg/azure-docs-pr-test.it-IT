---
title: "aaaDesign servizio a disponibilità elevata utilizzando il Database SQL di Azure | Documenti Microsoft"
description: "Informazioni sulla progettazione di applicazioni per servizi a disponibilità elevata con database SQL di Azure."
keywords: "ripristino di emergenza cloud, soluzioni di ripristino di emergenza, backup dei dati delle app, replica geografica, pianificazione della continuità aziendale"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: e8a346ac-dd08-41e7-9685-46cebca04582
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 04/21/2017
ms.author: sashan
ms.openlocfilehash: 815f754ba7014cd8a1108a2d84c2a8f71d7030a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-services-using-azure-sql-database"></a>Progettazione di servizi a disponibilità elevata con database SQL di Azure

Per compilare e distribuire servizi a disponibilità elevata in un Database SQL di Azure, utilizzare [failover gruppi e replica geografica attiva](sql-database-geo-replication-overview.md) errori di tooregional tooprovide resilienza e irreversibile interruzioni e abilitare rapido ripristino toohello database secondari. In questo articolo è incentrato sui modelli di applicazione comuni e ne illustra vantaggi hello e i vantaggi e svantaggi di ogni opzione a seconda dei requisiti di distribuzione dell'applicazione hello, hello contratto di servizio di destinazione, la latenza di traffico e costi. Per informazioni sulla replica geografica attiva con i pool elastici, vedere [Strategie di ripristino di emergenza per applicazioni che usano il pool elastico del database SQL](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

## <a name="design-pattern-1-active-passive-deployment-for-cloud-disaster-recovery-with-a-co-located-database"></a>Modello di progettazione 1: distribuzione attiva/passiva per il ripristino di emergenza cloud mediante un database con percorso condiviso
Questa opzione è più adatta per le applicazioni con hello seguenti caratteristiche:

* Istanza attiva in una singola area di Azure
* Dipendenza sicura toodata di accesso in lettura / scrittura (lettura/scrittura)
* La connettività tra più aree tra un'applicazione web hello e database hello non è accettabile a causa dei costi di traffico e toolatency    

In questo caso, topologia di distribuzione dell'applicazione hello è ottimizzata per la gestione di calamità quando tutti i componenti dell'applicazione sono interessati ed è necessario toofailover come unità. Per garantire ridondanza geografica, la logica dell'applicazione hello e database hello sono replicati tooanother area ma non vengono usati per carico di lavoro dell'applicazione hello in condizioni normali hello. un'applicazione Hello nell'area secondaria hello deve essere configurato toouse in un database secondario SQL connection string toohello. Gestione traffico è configurato toouse [metodo di routing failover](../traffic-manager/traffic-manager-configure-failover-routing-method.md).  

> [!NOTE]
> [Gestione traffico di Azure](../traffic-manager/traffic-manager-overview.md) viene usato in questo articolo solo a scopi illustrativi. È possibile usare qualsiasi soluzione di bilanciamento del carico che supporta il metodo di routing di failover.    
>

Hello seguente diagramma viene illustrata questa configurazione prima di un'interruzione del servizio.

![Configurazione della replica geografica del database SQL. Ripristino di emergenza cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-1.png)

Dopo un'interruzione nell'area primaria hello, il servizio di Database SQL di hello rileva tale database primario hello non è accessibile e attivare un database secondario toohello failover in base ai parametri di hello dei criteri di failover automatico hello. A seconda del contratto di servizio dell'applicazione, è possibile decidere di tooconfigure un periodo di tolleranza tra rilevamento hello di interruzione hello e failover hello stesso. Configurazione di un periodo di tolleranza riduce il rischio di hello di casi di toohello perdita di dati dove interruzione hello è irreversibile e disponibilità in area hello non può essere ripristinata rapidamente. Se hello failover dell'endpoint viene avviato da Gestione traffico hello prima che i trigger di hello failover gruppo hello failover del database di hello, un'applicazione hello web non è in grado di tooreconnect toohello database. tooreconnect tentativo dell'applicazione Hello viene completata automaticamente non appena viene completato hello failover del database. 

> [!NOTE]
> tooachieve coordinato completamente failover dell'applicazione hello e i database di hello, è necessario definire il proprio metodo di monitoraggio e utilizzare il failover manuale di endpoint dell'applicazione web hello e database di hello.
>

Al termine del processo di failover di hello dell'applicazione hello endpoint sia database hello, un'applicazione hello nuovamente avvierà l'elaborazione delle richieste utente hello in area hello B e rimarrà collocata insieme ai database hello database primario hello è ora in area B. Questo scenario è illustrato nel seguente diagramma hello. In tutti i diagrammi le linee continue indicano le connessioni attive, le linee con punti indicano le connessioni sospese e i segnali di stop indicano i trigger di azioni.

![La replica geografica: Il Failover toosecondary del database. Backup dei dati delle app.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-2.png)

In caso di un'interruzione del servizio nell'area secondaria hello, hello collegamento di replica tra hello primario e secondario hello viene sospeso ma hello failover non viene generato perché il database primario hello non è compromessa. disponibilità dell'applicazione Hello non viene modificata in questo caso, ma un'applicazione hello opera esposto e pertanto a rischio più elevato nel caso in entrambe le aree esito negativo in successione.

> [!NOTE]
> Per il ripristino di emergenza è consigliabile configurazione hello con aree tootwo distribuzione limitata di applicazione. In questo modo la maggior parte di hello aree geografiche di Azure sono solo due aree. Questa configurazione non proteggerà l'applicazione da un errore simultaneo irreparabile di entrambe le aree.  Nell'improbabile eventualità di un errore di questo genere, è possibile recuperare i database in una terza area con un'[operazione di ripristino geografico](sql-database-disaster-recovery.md#recover-using-geo-restore).
>

Dopo un'interruzione di hello viene ridotta, database secondario hello verrà automaticamente nuovamente la sincronizzazione con hello primario. Durante la sincronizzazione, le prestazioni di hello primaria possono essere interessate leggermente a seconda della quantità di hello di dati che devono essere toobe sincronizzato. Hello diagramma seguente illustra un'interruzione del servizio nell'area secondaria hello.

![Database secondario sincronizzato con il database primario. Ripristino di emergenza cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-3.png)

chiave Hello **vantaggi** di questo schema progettuale sono:

* Hello stessa applicazione web viene distribuito tooboth aree senza alcuna configurazione specifiche dell'area e di failover di toohello tooreact alcuna logica aggiuntiva. 
* le prestazioni dell'applicazione Hello non venga interessata da failover come applicazione web hello e database hello sono sempre posizionati.

Hello principale **compromesso** è che un'applicazione hello ridondanti istanza nell'area secondaria hello viene utilizzata solo per il ripristino di emergenza.

## <a name="design-pattern-2-active-active-deployment-for-application-load-balancing"></a>Modello di progettazione 2: Distribuzione attiva/attiva per il bilanciamento del carico dell'applicazione
Questa opzione di ripristino di emergenza cloud è ideale per applicazioni con hello seguenti caratteristiche:

* Rapporto elevato di database legge toowrites
* Database latenza di lettura è più importanti per un'esperienza utente finale hello la latenza di scrittura hello 
* Logica di sola lettura che può essere separata dalla logica di lettura/scrittura usando una stringa di connessione diversa
* La logica di sola lettura non dipendono dai dati completamente sincronizzati con gli aggiornamenti più recenti di hello  

Se le applicazioni presentano le caratteristiche, bilanciamento del carico le connessioni dell'utente finale di hello tra più istanze dell'applicazione in aree diverse possono migliorare notevolmente le hello complessiva dell'utente finale. Due delle aree di hello selezionata deve essere hello coppia di ripristino di emergenza e il gruppo di failover di hello deve includere i database hello in queste aree. tooimplement bilanciamento del carico, ogni area deve essere un'istanza attiva di un'applicazione hello con hello lettura-scrittura (lettura/scrittura) logica connessa toohello lettura-scrittura listener endpoint hello del gruppo del failover. Garantisce che il failover hello sarà avviato automaticamente se il database primario hello è stata interessata da un'interruzione del servizio. Hello sola lettura logica (RO) in un'applicazione web hello debba connettersi direttamente il database toohello in tale area. Gestione traffico deve essere configurato toouse [prestazioni routing](../traffic-manager/traffic-manager-configure-performance-routing-method.md) con [monitoraggio endpoint](../traffic-manager/traffic-manager-monitoring.md) abilitato per ogni istanza dell'applicazione.

È consigliabile distribuire un'applicazione di monitoraggio simile a quella del modello n. 1, A differenza modello #1, hello monitoraggio dell'applicazione non verrà tuttavia responsabile per l'attivazione di failover di endpoint hello.

> [!NOTE]
> Mentre in questo modello viene utilizzato più di un database secondario, solo hello secondario area b viene utilizzata per il failover e deve far parte del gruppo di failover hello.
>

Gestione traffico deve essere configurato per la posizione geografica prestazioni routing toodirect hello utente connessioni toohello istanza più vicino toohello dell'utente dell'applicazione. Hello seguente diagramma viene illustrata questa configurazione prima di un'interruzione del servizio.

![Nessuna interruzione: applicazione toonearest routing delle prestazioni. Replica geografica.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-1.png)

Se viene rilevata un'interruzione del database paese hello, il gruppo di failover di hello avvierà automaticamente il failover del database primario hello toohello area secondaria nell'area B. Hello in lettura / scrittura listener endpoint tooregion B si aggiornerà automaticamente anche in modo non saranno interessate connessioni di lettura / scrittura in un'applicazione web hello. gestione traffico Hello escluderà endpoint offline hello dalla tabella di routing hello ma continuerà routing hello dell'utente finale traffico toohello rimanenti istanze online. salve le stringhe di connessione SQL in sola lettura non saranno interessate come puntano sempre database toohello in hello stessa area. 

Hello seguente diagramma illustra una nuova configurazione di hello dopo il failover hello.

![Configurazione dopo il failover. Ripristino di emergenza cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-2.png)

In caso di interruzione in una delle aree secondarie hello, gestione traffico hello rimuoverà automaticamente endpoint offline hello in tale regione dalla tabella di routing hello. Hello replica canale toohello database secondario in tale area verrà sospesi. Poiché le altre aree hello ottengono il traffico utente aggiuntivi in questo scenario, le prestazioni dell'applicazione hello saranno interessate durante un'interruzione di hello. Dopo un'interruzione di hello viene ridotta, hello database secondario nell'area interessata hello verrà immediatamente sincronizzata con hello primario. Durante la hello prestazioni di sincronizzazione di hello primaria possono essere interessate leggermente a seconda della quantità di hello di dati che devono essere sincronizzati toobe. Hello seguente diagramma viene illustrata un'interruzione nell'area B.

![Interruzione nell'area secondaria. Ripristino di emergenza cloud - Replica geografica.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-3.png)

chiave Hello **vantaggio** di questo progetto di modello è che è possibile scalare il carico di lavoro dell'applicazione hello tra le prestazioni ottimali per l'utente finale di più database secondari tooachieve hello. Hello **compromessi** di questa opzione sono:

* Le connessioni di lettura / scrittura tra le istanze dell'applicazione hello e database hanno latenza e i costi vari
* Le prestazioni dell'applicazione sono stata interessata durante un'interruzione di hello

> [!NOTE]
> Può essere utilizzato un approccio simile toooffload specializzato, ad esempio reporting processi, strumenti di business intelligence o i backup dei carichi di lavoro. In genere, questi carichi di lavoro utilizzano le risorse del database significativo per questo motivo è consigliabile che per designare una di hello database secondari per tali con carico di lavoro previsto hello prestazioni livello toohello corrispondente.
>

## <a name="design-pattern-3-active-passive-deployment-for-data-preservation"></a>Modello di progettazione 3: Distribuzione attiva/passiva per la conservazione dei dati
Questa opzione è più adatta per le applicazioni con hello seguenti caratteristiche:

* Qualsiasi perdita di dati rappresenta un rischio aziendale elevato. failover del database Hello sono utilizzabili solo come ultima risorsa se l'interruzione di hello è irreversibile.
* un'applicazione Hello supporta le modalità di sola lettura e lettura / scrittura delle operazioni e può essere utilizzato in "modalità di sola lettura" per un periodo di tempo.

In questo modello di applicazione hello passa tooread modalità di sola quando le connessioni di lettura / scrittura hello iniziano a ottenere gli errori di timeout. Hello applicazione Web viene distribuito tooboth aree e includere un endpoint della connessione toohello listener di lettura / scrittura e l'endpoint di connessione diverse toohello listener di sola lettura. gestione traffico Hello deve essere configurate toouse [failover routing](../traffic-manager/traffic-manager-configure-failover-routing-method.md) con [monitoraggio endpoint](../traffic-manager/traffic-manager-monitoring.md) abilitata per l'endpoint dell'applicazione hello in ogni area.

Hello seguente diagramma viene illustrata questa configurazione prima di un'interruzione del servizio.

![Distribuzione attiva-passiva prima del failover. Ripristino di emergenza cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-1.png)

Quando Gestione traffico hello rileva un tooregion di errore di connettività A, si passa automaticamente l'istanza dell'applicazione utente traffico toohello nell'area B. Con questo modello, è importante impostare il periodo di tolleranza hello con valore sufficientemente elevato tooa perdita dei dati, ad esempio, 24 ore. Garantisce che la perdita di dati, viene evitata se interruzione hello è attenuata entro tale periodo di tempo. Quando viene attivata l'applicazione Web nell'area di hello B hello operazioni di lettura-scrittura hello ha esito negativo. A questo punto, è necessario passare toohello modalità di sola lettura. In hello questa modalità, le richieste verranno automaticamente indirizzato toohello database secondario. Nel caso di hello di hello un errore irreversibile interruzione non essere risolti entro il periodo di prova hello e gruppo di failover hello attiverà hello failover. Dopo tale hello listener di lettura / scrittura diventerà disponibile e verrà arrestata hello chiamate tooit esito negativo. Questo comportamento è illustrato hello seguente diagramma.

![Interruzione: applicazione in modalità di sola lettura. Ripristino di emergenza cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-2.png)

Se l'interruzione di hello nell'area primaria hello è attenuata entro il periodo di prova hello, gestione traffico rileva ripristino hello di connettività area primaria hello e passa l'istanza dell'applicazione utente traffico toohello indietro nell'area A. Istanza di applicazione riprende e opera in modalità di lettura / scrittura utilizzando i database primario hello nell'area A.

In caso di interruzione nell'area di hello B, gestione traffico hello rileva gli errori di hello del punto finale dell'applicazione hello in area B e hello failover gruppo commutatori hello listener di sola lettura tooregion A. Questa interruzione non influisce sull'esperienza dell'utente finale di hello ma verrà esposto database primario hello durante un'interruzione di hello. Questo comportamento è illustrato hello seguente diagramma.

![Interruzione: database secondario. Ripristino di emergenza cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-3.png)

Una volta interruzione hello viene ridotta, hello database secondario viene immediatamente sincronizzata con hello primario e i listener di sola lettura hello viene switch toohello indietro il database secondario nell'area B. Durante la sincronizzazione delle prestazioni di hello primaria possono essere interessate leggermente a seconda della quantità di hello di dati che devono essere toobe sincronizzato.

Questo modello di progettazione presenta diversi **vantaggi**:

* Evita la perdita di dati durante le interruzioni temporanee hello.
* Tempo di inattività dipende dal solo la rapidità con gestione traffico rileva un errore di connettività hello, che è configurabile.

Hello **compromesso** è:

* Applicazione deve essere in grado di toooperate in modalità di sola lettura.

> [!NOTE]
> In caso di un'interruzione del servizio permanente nell'area di hello, manualmente attivare failover del database e la perdita di dati hello. un'applicazione Hello saranno funzionale nell'area secondaria di hello con database toohello accesso in lettura-scrittura.
>

## <a name="business-continuity-planning-choose-an-application-design-for-cloud-disaster-recovery"></a>Pianificazione della continuità aziendale: Scegliere una progettazione di applicazioni per il ripristino di emergenza cloud
La strategia di ripristino di emergenza cloud specifico è possibile combinare o estendere questi schemi progettuali toobest hello soddisfare le esigenze dell'applicazione.  Come accennato in precedenza, strategia hello che scelta si basa su hello contratto di servizio desiderato toooffer tooyour clienti e hello topologia di distribuzione dell'applicazione. toohelp facilitare la decisione, hello nella tabella seguente confronta scelte di hello in base a hello dati stimata perdita o ripristino obiettivo del punto (RPO) e il tempo di recupero stimato (ERT).

| Modello | RPO | ERT |
|:--- |:--- |:--- |
| Distribuzione attiva/passiva per il ripristino di emergenza con accesso al database con percorso condiviso |Accesso in lettura/scrittura < 5 sec |Ora di rilevamento dell'errore + DNS TTL |
| Distribuzione attiva/attiva per il bilanciamento del carico dell'applicazione |Accesso in lettura/scrittura < 5 sec |Ora di rilevamento dell'errore + DNS TTL |
| Distribuzione attiva/passiva per la conservazione dei dati |Accesso in sola lettura < 5 sec | Accesso in sola lettura = 0 |
||Accesso in lettura/scrittura = zero | Accesso in lettura-scrittura = ora di rilevamento dell'errore + periodo di tolleranza con perdita di dati |
|||

## <a name="next-steps"></a>Passaggi successivi
* toolearn sui backup di Database di SQL Azure automatizzati, vedere [backup automatici di Database SQL](sql-database-automated-backups.md)
* Per la panoramica e gli scenari della continuità aziendale, vedere [Continuità aziendale del database SQL di Azure](sql-database-business-continuity.md)
* toolearn sull'utilizzo di backup automatico per il ripristino, vedere [ripristinare un database dai backup avviate dal servizio hello](sql-database-recovery-using-backups.md)
* toolearn sulle opzioni di ripristino più veloce, vedere [replica geografica attiva](sql-database-geo-replication-overview.md)  
* toolearn sull'utilizzo di backup automatico per l'archiviazione, vedere [copia del database](sql-database-copy.md)
* Per informazioni sulla replica geografica attiva con i pool elastici, vedere [Strategie di ripristino di emergenza per applicazioni che usano il pool elastico del database SQL](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
