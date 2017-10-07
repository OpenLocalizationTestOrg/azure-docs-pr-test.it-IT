---
title: soluzioni di ripristino di emergenza aaaDesign - Database SQL di Azure | Documenti Microsoft
description: Informazioni su come toodesign la soluzione di cloud di ripristino di emergenza scegliendo il criterio di failover destra hello.
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2db99057-0c79-4fb0-a7f1-d1c057ec787f
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 9d9eca7570c7a01c992d0b33d449721709b471c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-strategies-for-applications-using-sql-database-elastic-pools"></a>Strategie di ripristino di emergenza per applicazioni che usano i pool elastici del database SQL
Negli anni hello è abbiamo appreso che i servizi cloud non sono infallibile e il verificarsi di eventi imprevisti irreversibili. Database SQL fornisce diverse funzionalità tooprovide per la continuità aziendale hello dell'applicazione quando si verificano gli eventi imprevisti. [Pool elastici](sql-database-elastic-pool.md) e singoli database supportano hello stesso tipo di ripristino di emergenza. Questo articolo illustra alcune strategie di ripristino di emergenza per i pool elastici che sfruttano i vantaggi di queste funzionalità per la continuità aziendale del database SQL.

In questo articolo Usa hello seguente modello di applicazione SaaS ISV canonico:

<i>Un'applicazione web basato su cloud moderne esegue il provisioning di un database SQL per ogni utente finale. Hello ISV ha molti clienti e pertanto Usa numerosi database, noti come database tenant. Poiché i database tenant hello dispongono in genere di modelli di attività imprevedibili, hello ISV utilizza un pool elastico toomake hello costo del database molto stimabile per periodi prolungati di tempo. pool elastico Hello semplifica anche la gestione delle prestazioni hello quando picchi di attività utente hello. Inoltre un'applicazione hello database tenant toohello utilizza diversi database profili utente mobili toomanage, sicurezza, raccolgono di modelli di utilizzo e così via. Disponibilità di singoli tenant hello non influisce sulla disponibilità dell'applicazione hello nel suo complesso. Tuttavia, hello disponibilità e prestazioni di database di gestione è critici per la funzione dell'applicazione hello e se il database di gestione di hello intera applicazione hello offline è offline.</i>  

In questo articolo vengono illustrate le strategie di ripristino di emergenza che coprono una gamma di scenari dal costo sensibili avvio applicazioni tooones con requisiti rigorosi di disponibilità.

## <a name="scenario-1-cost-sensitive-startup"></a>Scenario 1. Start-up attente ai costi
<i>Una start-up estremamente attenta ai costi  Desidero toosimplify distribuzione e gestione di un'applicazione hello e ho è un contratto di servizio limitato per i singoli clienti. Ma si desidera un'applicazione hello tooensure mai è offline.</i>

requisito di semplicità toosatisfy hello, distribuire tutti i database tenant in un pool elastico in hello Azure regione di propria scelta e i database di gestione come replica geografica singoli database. Per il ripristino di emergenza hello di tenant, usare il ripristino a livello geografico, viene fornito senza alcun costo aggiuntivo. disponibilità di hello tooensure di hello i database di gestione, abilitare la replica geografica li area tooanother usando un gruppo con failover automatico (in anteprima) (passaggio 1). costo Hello della configurazione di ripristino di emergenza hello in questo scenario è toohello uguale costo totale dei database secondari hello. Questa configurazione è illustrata nel diagramma successivo hello.

![Figura 1](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-1.png)

Se si verifica un'interruzione nell'area primaria hello, hello toobring passaggi di ripristino in linea l'applicazione vengono illustrato nel diagramma seguente hello.

* gruppo di failover Hello avvia il failover automatico dell'area del ripristino di emergenza toohello hello gestione database. un'applicazione Hello è toohello riconnessa automaticamente nuovi primario e tutti i nuovi account e i database tenant vengono creati nell'area di ripristino di emergenza hello. i clienti esistenti di Hello di visualizzare i dati temporaneamente non disponibili.
* Creare il pool elastico di hello con hello stessa configurazione di pool originale hello (2).
* Utilizzare il ripristino geografico toocreate copie dei database tenant hello (3). È possibile prendere in considerazione l'attivazione di ripristini singoli hello per le connessioni dell'utente finale di hello o utilizzare altri schemi di priorità specifico dell'applicazione.


A questo punto l'applicazione è in modalità online nell'area di ripristino di emergenza hello, ma alcuni clienti ritardo durante l'accesso ai dati.

![Figura 2](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-2.png)

Se l'interruzione di hello è temporanea, è possibile che tale area primaria hello viene recuperato da Azure prima del completamento tutti i ripristini di database hello in area hello ripristino di emergenza. In questo caso, orchestrare lo spostamento hello applicazione back-toohello area primaria. il processo di Hello richiede passaggi hello illustrati nel diagramma successivo hello.

* Annullare tutte le richieste di ripristino geografico in sospeso.   
* Eseguire il failover hello management database toohello area primaria (5). Dopo il ripristino dell'area di hello, primari precedente hello diventate automaticamente i database secondari. Ora i ruoli vengono nuovamente invertiti. 
* Modificare l'area geografica primaria dell'applicazione hello connessione stringa toopoint toohello indietro. Ora tutti i nuovi account e i database tenant vengono creati nell'area primaria hello. I dati risultano temporaneamente non disponibili per alcuni clienti esistenti.   
* Impostare tutti i database in hello ripristino di emergenza pool solo tooread tooensure che non possono essere modificate nell'area di ripristino di emergenza hello (6). 
* Per ogni database nel pool di ripristino di emergenza che è stato modificato dopo il recupero di hello hello, rinominare o eliminare i database corrispondenti hello in pool primario hello (7). 
* Hello copia aggiornato i database da hello pool primario di toohello pool ripristino di emergenza (8). 
* Eliminare il pool di ripristino di emergenza hello (9)

A questo punto l'applicazione è online nell'area primaria di hello con tutti i tenant database disponibili nel pool primario hello.

![Figura 3](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-3.png)

chiave Hello **vantaggio** di questa strategia è basso costo per la ridondanza del livello dati. I backup vengono eseguiti automaticamente dal servizio di Database SQL con nessun riscrittura dell'applicazione e senza alcun costo aggiuntivo hello.  costo Hello si verifica solo quando vengono ripristinati i database elastici hello. Hello **compromesso** ripristino completo di hello di tutti i database di tenant accettati molto tempo. Hello periodo di tempo dipende dal numero totale di hello di ripristini si avvia in hello ripristino di emergenza area e la dimensione complessiva di hello tenant di database. Anche se è la priorità ripristini alcuni tenant rispetto alle altre, sono in competizione con hello tutti gli altri ripristini avviati in hello stessa area come servizio hello regola e limita toominimize hello impatto complessivo sui database hello clienti esistenti. Inoltre, ripristino hello del database tenant hello non è possibile avviare fino a quando non viene creato nuovo pool elastico hello nell'area di ripristino di emergenza hello.

## <a name="scenario-2-mature-application-with-tiered-service"></a>Scenario 2. Applicazione matura con più livelli di servizio
<i>Un'applicazione SaaS matura con più livelli di offerte del servizio e diversi contratti di servizio per i clienti delle versioni di valutazione e i clienti delle versioni a pagamento Per i clienti di valutazione di hello, è necessario tooreduce hello costo quanto possibile. I clienti di valutazione possono richiedere tempi di inattività, ma si desidera tooreduce relativa probabilità. Per i clienti paganti di hello, eventuali tempi di inattività implica un rischio di volo. Pertanto si desidera che i clienti paganti siano sempre in grado di tooaccess toomake i propri dati.</i> 

toosupport questo scenario, separato hello tenant da pagamento tenant inserendole in pool elastici separato. i clienti di valutazione di Hello hanno inferiore eDTU per ogni tenant e un contratto di servizio inferiore con un tempo di ripristino. per i clienti paganti Hello sono in un pool con maggiore eDTU per ogni tenant e un contratto di servizio superiore. tooguarantee hello minimo tempo di recupero, i database tenant dei clienti paganti hello vengono replicati geograficamente. Questa configurazione è illustrata nel diagramma successivo hello. 

![Figura 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-4.png)

Come primo scenario hello, i database di gestione di hello sono piuttosto attivi in modo da utilizzare un singolo database di replica geografica per tale (1). In questo modo si garantisce prestazioni prevedibili di hello per le nuove sottoscrizioni dei clienti, aggiornamenti a un profilo e altre operazioni di gestione. area in cui risiedono i colori hello del database di gestione di hello Hello è area primaria hello e hello l'area in cui risiedono i database secondari hello del database di gestione di hello è area di hello ripristino di emergenza.

Hello tenant database i clienti paganti dispongono di un database attivo in pool, il provisioning nell'area primaria hello "pagamento" hello. Eseguire il provisioning di un pool con stesso nome nell'area di ripristino di emergenza hello hello secondario. Ogni tenant è toohello replica geografica secondaria pool (2). Ciò consente un ripristino rapido di tutti i database tenant con il failover. 

Se si verifica un'interruzione nell'area primaria hello, hello toobring passaggi di ripristino in linea l'applicazione sono illustrati nel diagramma successivo hello:

![Figura 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-5.png)

* Failover immediatamente l'area del ripristino di emergenza toohello database Gestione hello (3).
* Modificare l'area del ripristino di emergenza toohello toopoint stringa connessione dell'applicazione hello. Ora tutti i nuovi account e i database tenant vengono creati nell'area di ripristino di emergenza hello. i clienti esistenti valutazione Hello di visualizzare i dati temporaneamente non disponibili.
* Eseguire il failover a pagamento database toohello pool del tenant hello ripristino di emergenza area tooimmediately hello ripristinare la disponibilità (4). Poiché il failover hello è una modifica del livello di metadati rapido, prendere in considerazione un'ottimizzazione in cui i failover singoli hello vengono attivati su richiesta per le connessioni dell'utente finale di hello. 
* Se la dimensione di eDTU del pool secondario era inferiore a quello primario hello perché i database secondari di hello solo hello necessarie capacità tooprocess hello Modifica log durante la sono stati di database secondari immediatamente aumenta la capacità del pool di hello ora tooaccommodate hello completo carico di lavoro di tutti i tenant (5). 
* Creare pool elastico nuova hello con hello stesso nome e hello stessa configurazione nell'area di hello ripristino di emergenza per i database dei clienti valutazione hello (6). 
* Una volta creato il pool di hello valutazione dei clienti, utilizzare i database di ripristino a livello geografico toorestore hello singoli tenant di prova nel nuovo pool di hello (7). Attivazione di ripristini singoli hello per le connessioni dell'utente finale di hello oppure usare altri schemi di priorità specifico dell'applicazione.

A questo punto l'applicazione è in modalità online nell'area di ripristino di emergenza hello. Tutti i clienti paganti dispongono di accesso ai dati tootheir mentre i clienti di valutazione di hello ritardo durante l'accesso ai dati.

Quando verrà ripristinato area primaria hello Azure *dopo* è stato ripristinato di un'applicazione hello in area hello ripristino di emergenza è possibile continuare l'esecuzione di un'applicazione hello in tale area oppure è possibile decidere area primaria di toofail toohello indietro. Se viene ripristinato l'area primaria hello *prima* completamento del processo di failover hello, si consiglia di non superati back immediatamente. il failback Hello esegue i passaggi di hello illustrati nel diagramma successivo hello: 

![Figura 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-6.png)

* Annullare tutte le richieste di ripristino geografico in sospeso.   
* Il failover dei database di gestione di hello (8). Dopo il ripristino dell'area di hello, hello primario precedente diventa automaticamente hello secondario. Ora diventa hello nuovo primario.  
* Eseguire il failover hello a pagamento database tenant (9). Analogamente, dopo il ripristino dell'area di hello, primari precedente hello diventano automaticamente repliche secondarie hello. Ora diventano primari hello nuovamente. 
* Set hello ripristinato i database di prova che sono state modificate nell'area di ripristino di emergenza hello solo tooread (10).
* Per ogni database nel pool di ripristino di emergenza di clienti valutazione hello modificato dopo il recupero di hello, rinominare o eliminare database corrispondente di hello in pool primario clienti valutazione hello (11). 
* Hello copia aggiornato i database da hello pool primario di toohello pool ripristino di emergenza (12). 
* Eliminare il pool di ripristino di emergenza hello (13) 

> [!NOTE]
> l'operazione di failover Hello è asincrona. tempo di recupero hello toominimize che è importante eseguire il comando di failover dei database tenant hello in batch di almeno 20 database. 
> 
> 

chiave Hello **vantaggio** di questa strategia è quello di fornire hello contratto di servizio più elevata per i clienti paganti hello. Garantisce inoltre che le versioni di valutazione nuovo hello sono bloccati non appena viene creato hello valutazione pool di ripristino di emergenza. Hello **compromesso** è che il programma di installazione aumento hello del costo totale del database tenant hello dal costo hello del pool di ripristino di emergenza secondario di hello per a pagamento di clienti. Inoltre, se pool secondario hello è di dimensioni diverse, i clienti paganti hello prestazioni inferiore dopo il failover fino a quando non hello pool nell'area di ripristino di emergenza hello completato l'aggiornamento. 

## <a name="scenario-3-geographically-distributed-application-with-tiered-service"></a>Scenario 3. Applicazione geograficamente distribuita con più livelli di servizio
<i>Un'applicazione SaaS matura con offerte di più livelli di servizio Si desidera toooffer un aggressivo toomy contratto di servizio a pagamento di clienti e ridurre al minimo il rischio di hello di impatto quando si verificano interruzioni poiché anche breve interruzione può causare l'insoddisfazione dei clienti. È fondamentale che i clienti paganti di hello può accedere sempre ai dati. sono disponibili le versioni di valutazione di Hello e un contratto di servizio non è disponibile durante il periodo di valutazione di hello.</i> 

toosupport questo scenario, utilizzare tre separato elastico pool. Eseguire il provisioning due pool di uguale dimensione con elevato numero di Edtu per ogni database di hello di toocontain due aree diverse a pagamento database tenant dei clienti. pool di terzo Hello contenente tenant hello può avere inferiore Edtu per database ed eseguirne il provisioning in uno dei due aree hello.

tooguarantee hello minimo tempo di recupero durante le interruzioni, i database tenant dei clienti paganti hello vengono replicati geograficamente con il 50% dei database primari di hello in ognuna delle aree di hello due. Analogamente, ogni regione è 50% dei database secondari hello. In questo modo, se un'area è offline, solo il 50% di hello a pagamento database dei clienti sono interessati e abbia toofail. Hello altri database rimangono invariato. Questa configurazione è illustrata nel seguente diagramma hello:

![Figura 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-7.png)

Come negli scenari precedenti hello, i database di gestione di hello attivi piuttosto quindi configurarli come singolo database di replica geografica (1). In questo modo si garantisce prestazioni prevedibili di hello di nuove sottoscrizioni di cliente hello, aggiornamenti a un profilo e altre operazioni di gestione. Area è area primaria di hello per il database di gestione di hello e area hello B viene utilizzata per il ripristino dei database di gestione di hello.

i database tenant dei clienti paganti Hello inoltre vengono replicati geograficamente, ma con colori primari e secondari suddivisa tra paese e area B (2). In questo modo, il database primario di hello tenant interessato dall'interruzione hello possono eseguire il failover toohello altre aree e rese disponibili. Hello altri metà del database tenant hello non sono interessati affatto. 

nel diagramma seguente Hello illustra hello ripristino passaggi tootake se si verifica un'interruzione nell'area A.

![Figura 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-8.png)

* Il failover immediatamente hello management database tooregion B (3).
* Modifica connessione stringa toopoint toohello i database di gestione dell'applicazione hello nell'area B. modifica hello management database toomake che hello nuovi account e i database tenant vengono creati nell'area B e sono presenti database tenant esistenti hello come e. i clienti esistenti valutazione Hello di visualizzare i dati temporaneamente non disponibili.
* Eseguire il failover a pagamento toopool di database di tenant 2 nell'area B tooimmediately hello ripristinare la disponibilità (4). Poiché il failover hello è una modifica del livello di metadati rapido, è possibile considerare un'ottimizzazione in cui i failover singoli hello vengono attivati su richiesta per le connessioni dell'utente finale di hello. 
* Poiché ora pool 2 contiene solo i database primari, hello totale del carico di lavoro di hello pool aumenta e immediatamente possibile aumentarne le dimensioni di eDTU (5). 
* Creare pool elastico nuova hello con hello stesso nome e hello stessa configurazione nell'area di hello B per i database dei clienti valutazione hello (6). 
* Una volta hello viene creato pool Usa ripristino a livello geografico toorestore hello tenant di prova singoli database nel pool di hello (7). È possibile prendere in considerazione l'attivazione di ripristini singoli hello per le connessioni dell'utente finale di hello o utilizzare altri schemi di priorità specifico dell'applicazione.

> [!NOTE]
> l'operazione di failover Hello è asincrona. tempo di recupero hello toominimize, è importante eseguire il comando di failover dei database tenant hello in batch di almeno 20 database. 
> 

A questo punto l'applicazione è in modalità online nell'area B. Tutti i clienti paganti dispongono di accesso ai dati tootheir mentre i clienti di valutazione di hello ritardo durante l'accesso ai dati.

Quando viene recuperato l'area A toodecide è necessario se si desidera che l'area B toouse per i clienti di valutazione o un pool di failback toousing hello valutazione clienti nell'area A. Un criterio potrebbe essere hello % dei database di tenant di prova modificato dopo il ripristino di hello. Indipendentemente dal fatto di tale decisione, è necessario tenant hello a pagamento toore bilanciamento tra due pool. nel diagramma seguente Hello illustra il processo di hello quando i database tenant di prova hello non riescono A. tooregion indietro  

![Figura 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-9.png)

* Annullare tutti i pool di tootrial ripristino di emergenza richieste ripristino a livello geografico in sospeso.   
* Eseguire il failover del database di gestione di hello (8). Dopo il ripristino dell'area di hello, primario precedente hello è diventato automaticamente hello secondario. Ora diventa hello nuovo primario.  
* Selezionare i database tenant a pagamento di esito negativo toopool back-1 e avviare il failover tootheir secondari (9). Dopo il ripristino dell'area di hello, tutti i database nel pool 1 è stato reso automaticamente le repliche secondarie. Ora il 50% dei database diventa di nuovo primario. 
* Ridurre le dimensioni di hello toohello 2 originale eDTU del (10).
* Tutti i set ripristinato i database di prova nell'area di hello B solo tooread (11).
* Per ogni database nel pool di ripristino di emergenza valutazione hello che è stato modificato dopo il recupero di hello, rinominare o eliminare database corrispondente di hello in pool primario valutazione hello (12). 
* Hello copia aggiornato i database da hello pool primario di toohello pool ripristino di emergenza (13). 
* Eliminare il pool di ripristino di emergenza hello (14) 

chiave Hello **vantaggi** di questa strategia sono:

* I clienti paganti poiché garantisce che un'interruzione del servizio in grado di influire più del 50% dei database tenant hello hello supporta il contratto di servizio più stringenti hello. 
* Garantisce che le versioni di valutazione nuovo hello sono bloccati appena creata durante il ripristino di hello trail hello pool di ripristino di emergenza. 
* Consente l'uso più efficiente della capacità del pool di hello al 50% di database secondari in un pool di applicazioni 1 e 2 pool vengono garantiti toobe meno attivi rispetto ai database primari hello.

Hello principale **compromessi** sono:

* le operazioni CRUD Hello nei database di gestione di hello abbia una latenza inferiore per hello gli utenti finali connessi tooregion A rispetto a per gli utenti finali connessi di hello tooregion B come essi vengono eseguite hello primario del database di gestione di hello.
* Richiede la progettazione più complessa hello del database di gestione. Ad esempio, ogni record tenant contiene un tag di percorso che deve toobe modificato durante il failover e failback.  
* i clienti paganti Hello prestazioni inferiore superiore al normale fino a quando non hello pool nell'area B completato l'aggiornamento. 

## <a name="summary"></a>Riepilogo
In questo articolo è incentrato sulle strategie di ripristino di emergenza hello per hello livello di database utilizzati da un'applicazione multi-tenant SaaS ISV. Hello strategia scelta è in base alle esigenze di hello dell'applicazione hello, ad esempio modello di business hello, Service Level AGREEMENT hello desiderati toooffer tooyour clienti, budget vincolo e così via. Vantaggi di strategia contorni hello e compromesso descritti in modo è possibile prendere una decisione consapevole. È anche probabile che l'applicazione specifica includa altri componenti di Azure. Per esaminare le informazioni sulla continuità aziendale e orchestrare ripristino hello del livello di database hello con essi. toolearn informazioni su gestione del ripristino di applicazioni di database in Azure, fare riferimento troppo[progettazione di soluzioni cloud per il ripristino di emergenza](sql-database-designing-cloud-solutions-for-disaster-recovery.md).  

## <a name="next-steps"></a>Passaggi successivi
* toolearn sui backup di Database di SQL Azure automatizzati, vedere [backup automatici di Database SQL](sql-database-automated-backups.md).
* Per la panoramica e gli scenari della continuità aziendale, vedere [Continuità aziendale del database SQL di Azure](sql-database-business-continuity.md).
* toolearn sull'utilizzo di backup automatico per il ripristino, vedere [ripristinare un database dai backup avviate dal servizio hello](sql-database-recovery-using-backups.md).
* toolearn sulle opzioni di ripristino più veloce, vedere [replica geografica attiva](sql-database-geo-replication-overview.md).
* toolearn sull'utilizzo di backup automatico per l'archiviazione, vedere [copia del database](sql-database-copy.md).

