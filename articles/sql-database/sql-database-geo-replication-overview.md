---
title: aaaFailover gruppi e replica geografica attiva - Database SQL di Azure | Documenti Microsoft
description: Gruppi con failover automatico con replica geografica attiva consente toosetup 4 repliche del database in uno dei Data Center di Azure hello e failover autoomatically nell'evento hello di interruzione.
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2a29f657-82fb-4283-9a83-e14a144bfd93
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 07/10/2017
ms.author: sashan
ms.openlocfilehash: 7a39af8505624c0f19c5abccff051af836b1f9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-failover-groups-and-active-geo-replication"></a>Panoramica: gruppi di failover e replica geografica attiva
Replica geografica attiva consente tooconfigure backup toofour database secondari leggibili in hello stesso o in diversi data center posizioni (aree). Database secondari sono disponibili per l'esecuzione di query e per il failover nel caso di hello di un data center hello o un'interruzione dell'impossibilità tooconnect toohello database primario. Hello failover deve essere avviato manualmente da un'applicazione hello dell'utente hello. Dopo il failover, nuovo database primario di hello dispone di un endpoint di connessione diversa. 

> [!NOTE]
> La replica geografica attiva è disponibile per tutti i database in tutti i livelli di servizio in tutte le aree.
>  

Gruppi con failover automatico di Database SQL Azure (in anteprima) è un tooautomatically funzionalità progettata SQL Database gestire relazione di replica geografica, connettività e il failover su larga scala. Con, hello clienti guadagno hello possibilità tooautomatically ripristinare più database correlati nell'area secondaria hello dopo errori internazionali irreversibili o altri eventi imprevisti che comportano la perdita parziale o completa di hello del servizio di Database SQL disponibilità nell'area primaria hello. Inoltre, usano hello database secondari leggibili toooffload sola lettura e i carichi di lavoro.  Poiché i gruppi con failover automatico implicano più database devono essere configurati nel server primario hello. Server primario e secondario devono appartenere hello stessa sottoscrizione. Gruppi con failover automatico supportano la replica di tutti i database in hello gruppo tooonly un server secondario in un'area diversa. Consente di replica geografica attiva, senza gruppi con failover automatico, le repliche secondarie too4 in qualsiasi area.

Se si utilizza la replica geografica attiva e per qualsiasi motivo che il database primario non riesce, o semplicemente i toobe esigenze portato offline, è possibile avviare tooany failover dei database secondari. Quando è attivata tooone dei database secondari hello un failover, tutte le altre repliche secondarie sono toohello automaticamente collegato nuovo database primario. Se si utilizza con failover automatico consente di raggruppare il recupero del database (in anteprima) toomanage e qualsiasi interruzione che influisce su uno o più database hello nei risultati di gruppo hello nel failover automatico. È possibile configurare i criteri di failover automatico hello che meglio soddisfano le esigenze dell'applicazione, oppure è possibile escludere e usare l'attivazione manuale. I gruppi di failover automatico (in anteprima) forniscono anche endpoint di listener di sola lettura e di sola scrittura che rimangono invariati durante i failover. Se si utilizza l'attivazione di failover manuale o automatico, failover passa tutti i database secondari in tooprimary gruppo hello. Al termine di failover del database hello, record DNS hello è tooredirect aggiornate automaticamente hello endpoint toohello nuova area.

È possibile gestire la replica e il failover di un singolo database o di un set di database in un server o in un pool elastico tramite la replica geografica attiva. È possibile eseguire tale utilizzando hello [portale di Azure](sql-database-geo-replication-portal.md), [PowerShell](sql-database-geo-replication-powershell.md), [Transact-SQL](sql-database-geo-replication-transact-sql.md), o hello [API REST](https://msdn.microsoft.com/library/azure/mt163685.aspx). Dopo il failover, verificare i requisiti di autenticazione hello per server e database sono configurati nel nuovo database primario di hello. Per tutti i dettagli, vedere l'articolo sulla [sicurezza del database SQL di Azure dopo il ripristino di emergenza](sql-database-geo-replication-security-config.md). Si applica sia tooactive con failover automatico e la replica geografica gruppi (in anteprima).

Hello sfrutta la replica geografica attiva [Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) tecnologia di SQL Server tooasynchronously replicare il commit delle transazioni in hello database primario tooa database secondario tramite l'isolamento dello snapshot read committed (Read Committed). Gruppi con failover automatico forniscono la semantica di gruppo hello nella parte superiore di replica geografica attiva ma hello viene utilizzato il meccanismo di replica asincrona stessa. Anche se a un certo punto, database secondario hello potrà essere leggermente indietro rispetto database primario hello, hello viene garantito che toonever con transazioni parziale. La ridondanza tra aree consente applicazioni tooquickly di recupero dalla perdita definitiva di un intero Data Center o parti di un Data Center causata da calamità naturali, errori umani irreversibili o atti dolosi. dati RPO specifici Hello sono reperibile in [Panoramica di continuità aziendale](sql-database-business-continuity.md).

Hello figura riportata di seguito viene illustrato un esempio di replica geografica attiva configurato con un database primario nell'area di hello North Central US e secondari nell'area di hello centro-meridionali.

![relazione di replica geografica](./media/sql-database-active-geo-replication/geo-replication-relationship.png)

Poiché i database secondari hello sono leggibili, possono essere utilizzati toooffload sola lettura carichi di lavoro come processi di reporting. Se si utilizza la replica geografica attiva, è possibile toocreate database secondario di hello in hello stessa regione con hello primario, ma non aumenta errori toocatastrophic di resilienza dell'applicazione hello. Se si usano i gruppi di failover automatico (in anteprima), i database secondari vengono sempre creati in un'area diversa.

Inoltre toodisaster ripristino replica geografica attiva è utilizzabile nei seguenti scenari hello:

* **Migrazione di database**: È possibile utilizzare la replica geografica attiva toomigrate un database da un server tooanother online con tempo di inattività minimo.
* **Aggiornamenti dell'applicazione**: è possibile creare un database secondario aggiuntivo come copia di failback durante gli aggiornamenti dell'applicazione.

tooachieve reale continuità aziendale, l'aggiunta di ridondanza del database tra i Data Center è solo una parte della soluzione hello. Ripristino di un'applicazione (servizio) end-to-end dopo un errore irreversibile richiede il ripristino di tutti i componenti che costituiscono il servizio hello e dei servizi dipendenti. Esempi di questi componenti includono il software client hello (ad esempio, un browser con JavaScript personalizzato), front-end web, archiviazione e DNS. È fondamentale che tutti i componenti siano resiliente toohello stessi errori e diventano disponibili all'interno di hello obiettivo tempo di ripristino (RTO) dell'applicazione. Pertanto, è necessario tooidentify tutti i servizi dipendenti e comprendere hello garanzie e funzionalità che vengono fornite. Quindi, è necessario prendere provvedimenti tooensure che il funzionamento del servizio durante hello failover dei servizi di hello da cui dipende. Per altre informazioni sulla progettazione di soluzioni per il ripristino di emergenza, vedere [Progettazione di applicazioni per il ripristino di emergenza cloud con la replica geografica attiva in database SQL](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

## <a name="active-geo-replication-capabilities"></a>Funzionalità della replica geografica attiva
funzionalità di replica geografica attiva Hello fornisce hello funzioni essenziali seguenti:
* **Replica asincrona automatica**: È possibile creare solo un database secondario tramite l'aggiunta di database esistente tooan. è possibile creare Hello secondario in qualsiasi server di Database SQL di Azure. Una volta creato, database secondario hello viene popolata con dati hello copiati dal database primario hello. Questo processo è noto come seeding. Dopo aver creato ed effettuato il seeding del database secondario, gli aggiornamenti in modo asincrono è quello del database primario toohello replicati automaticamente toohello database secondario. La replica asincrona significa che le transazioni vengono sottoposte a commit sul database primario hello prima che vengano replicati toohello database secondario. 
* **Database secondari leggibili**: un'applicazione può accedere a un database secondario per operazioni di sola lettura utilizzando hello uguali o diverse identità di protezione utilizzato per accedere al database primario hello. Hello database secondari operano in isolamento dello snapshot modalità tooensure della replica degli aggiornamenti di hello di hello primaria (la riesecuzione del registro) non viene ritardato da query eseguite sul hello secondario.

   > [!NOTE]
   > la riesecuzione del Registro di Hello viene ritardato nel database secondario hello se sono presenti aggiornamenti dello schema che vengono ricevuti dal database primario che richiedono un blocco dello schema nel database secondario hello hello. 
   > 

* **Più repliche secondarie leggibili**: due o più database secondari aumenta la ridondanza e livello di protezione per i database primari hello e dell'applicazione. In presenza di più database secondari, un'applicazione hello rimane protetta anche se uno dei database secondari hello non riesce. Se è presente un solo database secondario e si verifica un errore, viene esposta un'applicazione hello toohigher rischio fino a quando non viene creato un nuovo database secondario.

   > [!NOTE]
   > Se si utilizza la replica geografica attiva toobuild un'applicazione distribuita a livello globale e necessario tooprovide di sola lettura accedere toodata in aree più di 4, è possibile creare secondaria di un database secondario (processo noto come concatenazione). In questo modo è possibile ottenere una scalabilità virtualmente illimitata della replica del database. Inoltre, concatenazione riduce il sovraccarico di hello di replica dal database primario hello. compromesso di Hello è intervallo di replica maggiore hello nei database secondari di hello più foglia. . 
   >

* **Supporto dei database del pool elastico**: la replica geografica attiva può essere configurata per qualsiasi database in qualsiasi pool elastico. database secondario Hello può essere in un altro pool elastico. Per i database regolari, hello secondario può essere un pool elastico e viceversa, purché i livelli di servizio hello sono hello stesso. 
* **Livello di prestazioni configurabile del database secondario hello**: un database secondario può essere creato con livello di prestazioni inferiore a quello di hello primario. Database primari e secondari sono necessari toohave hello stesso livello di servizio. Questa opzione non è consigliata per le applicazioni con elevata scrittura attività del database perché l'intervallo di replica maggiore hello aumenta il rischio di hello di perdita di dati sostanziali dopo un failover. Inoltre, dopo sulle prestazioni dell'applicazione hello failover fino a quando hello nuovo primario sono prestazioni più elevate tooa aggiornato livello. grafico di percentuale dei / o di log nel portale Azure Hello fornisce tooestimate un buon metodo hello a livello di prestazioni minimo di hello secondaria che è necessario toosustain hello replica load. Ad esempio, se il database primario è P6 (1000 DTU) e relativa percentuale i/o di log è 50% hello secondario richiede toobe almeno P4 (500 DTU). È inoltre possibile recuperare dati dei / o log hello utilizzando [resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) o [Sys.dm db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) viste di database.  Per ulteriori informazioni sui livelli di prestazioni di hello Database SQL, vedere [opzioni del Database SQL e le prestazioni](sql-database-service-tiers.md). 
* **Failover controllato dall'utente e il failback**: un database secondario può essere esplicitamente ruolo primario toohello disattivati in qualsiasi momento da un'applicazione hello o un utente di hello. Durante un hello interruzione reale opzione "non pianificato" deve essere utilizzata, che promuove immediatamente primaria hello toobe secondario. Quando hello primario consente di recuperare ed è disponibile nuovo sistema hello automaticamente hello segni ripristinare principale come un database secondario e aggiornarlo con nuovo database primario di hello. A causa di toohello natura asincrona di replica, una piccola quantità di dati può essere persa durante i failover non pianificati se un database primario ha esito negativo prima della replica hello più recenti modifiche toohello secondario. Quando un database primario con più database secondari viene eseguito il failover, il sistema hello riconfigura automaticamente le relazioni di replica hello e hello collegamenti rimanenti toohello repliche secondarie appena alzate di livello principale senza richiedere alcun intervento dell'utente. Dopo l'interruzione del servizio che ha causato il failover hello hello viene ridotta, potrebbe essere area primaria toohello applicazione hello tooreturn auspicabile. toodo, che deve essere richiamato il comando di failover di hello con hello opzione "pianificato". 
* **Sincronizzazione credenziali e le regole del firewall**: si consiglia di utilizzare [regole del firewall di database](sql-database-firewall-configure.md) per i database di replica geografica in modo da queste regole possono essere replicate con hello database tooensure tutti i database secondari sono Hello stesse regole firewall hello primario. Questo approccio Elimina hello necessario per i clienti toomanually configurare e gestire regole firewall nel server che ospitano i database primari e secondari hello. Analogamente, l'utilizzo [utenti del database indipendente](sql-database-manage-logins.md) per i dati di accesso garantisce i database primari e secondari dispongano sempre hello pertanto durante un failover, non c'è nessun interruzioni delle credenziali utente stesso scadenza toomismatches con account di accesso e password. Con l'aggiunta di hello di [Azure Active Directory](../active-directory/active-directory-whatis.md), i clienti possono gestire utente accesso tooboth database primario e secondario ed eliminando hello necessario per la gestione delle credenziali nei database completamente.

## <a name="auto-failover-group-capabilities"></a>Funzionalità dei gruppi di failover automatico

La funzionalità dei gruppi di failover automatico fornisce un'astrazione potente della replica geografica attiva grazie al supporto della replica a livello di gruppo e al failover automatico. Inoltre, rimuove stringa di connessione SQL hello necessità toochange hello dopo il failover, fornendo gli endpoint di listener aggiuntivo hello. 

* **Gruppo di failover**: è possibile creare uno o più gruppi di failover tra due server in aree diverse (server primario e secondario). Ogni gruppo può includere uno o più database ripristinate come un'unità nel caso in cui alcuni o tutti i database primari diventano non disponibili a causa di interruzione tooan nell'area primaria hello.  
* **Server primario**: un server che ospita i database primari di hello in un gruppo di failover hello.
* **Server secondario**: un server che ospita i database secondari di hello in un gruppo di failover hello. server secondario Hello non può essere hello server primario hello stessa area.
* **Aggiungere il gruppo di database toofailover**: È possibile inserire più database all'interno di un server o all'interno di un elastica pool in hello stesso gruppo di failover. Se si aggiunge un gruppo di toohello database autonomo, viene creato automaticamente un database secondario utilizzando hello stesso edizione e livello di prestazioni. Se il database primario hello è in un pool elastico, hello secondario viene creato automaticamente nel pool elastico hello con hello stesso nome. Se si aggiunge un database che dispone già di un database secondario nel server secondario hello, che la replica geografica viene ereditata dal gruppo hello.

   > [!NOTE]
   > Quando si aggiunge un database che dispone già di un database secondario in un server che non fa parte del gruppo di failover di hello, viene creato un nuovo database secondario nel server secondario hello. 
   >

* **Lettura e scrittura listener del gruppo di failover**: record CNAME DNS di un formato come  **&lt;failover-group-name&gt;. database.windows.net** che punta toohello URL del server primario corrente. Consente di hello in lettura / scrittura di applicazioni SQL tootransparently riconnettersi database primario toohello quando viene modificato hello primario dopo il failover. 
* **Listener di sola lettura del gruppo con failover**: record CNAME DNS di un formato come  **&lt;failover-group-name&gt;. secondary.database.windows.net** che fa riferimento l'URL del server secondario toohello. Consente di hello sola lettura applicazioni SQL tootransparently connettersi toohello database secondario utilizzando hello specificate regole di bilanciamento del carico. Facoltativamente è possibile specificare se si desidera hello sola lettura toobe traffico reindirizzamento automatico server primario toohello quando il server secondario hello non è disponibile.
* **Criteri di failover automatico**: per impostazione predefinita, il gruppo di failover di hello è configurato con un criterio di failover automatico. Hello sistema attiva il failover, non appena viene rilevato un errore di hello. Se si desidera toocontrol hello failover flusso di lavoro da un'applicazione hello, è possibile disattivare il failover automatico. 
* **Failover manuale**: È possibile avviare manualmente il failover in qualsiasi momento, indipendentemente dalla configurazione di failover automatico hello. Se i criteri di failover automatico non sono configurato il failover manuale è database toorecover obbligatorio in un gruppo di failover di hello. È possibile avviare il failover forzato o semplice (con sincronizzazione completa dei dati). Hello quest'ultimo potrebbe essere area primaria toohello toorelocate utilizzati hello server attivo. Quando viene completato il failover record DNS hello vengono aggiornate automaticamente tooensure connettività toohello corretto del server.
* **Periodo di prova con perdita di dati**: perché il database primario e secondario hello vengono sincronizzati mediante la replica asincrona hello failover può comportare la perdita di dati. È possibile personalizzare tooreflect criteri di failover automatico hello perdita toodata di tolleranza di errore dell'applicazione. Configurando **GracePeriodWithDataLossHours**, è possibile controllare il tempo di attesa prima dell'avvio del failover hello tooresult probabile perdita di dati di sistema hello. 

   > [!NOTE]
   > Quando system rileva che il database di hello in un gruppo di hello sono ancora online (ad esempio, interruzione hello solo interessati piano di controllo servizio hello), viene attivata immediatamente hello failover con la sincronizzazione completa dei dati (failover descrittivo) indipendentemente dal valore hello l'impostazione **GracePeriodWithDataLossHours**. Questo comportamento non assicura che sia presente alcuna perdita di dati durante il recupero di hello. il periodo di tolleranza Hello ha effetto solo quando un failover descrittivo non è possibile. Se l'interruzione hello viene ridotta prima della scadenza del periodo di tolleranza hello, hello failover non è attivato.
   >

* **Più gruppi di failover**: È possibile configurare più gruppi di failover per hello stessa coppia di scala di hello toocontrol server di failover. Ogni gruppo esegue il failover in modo indipendente. Se l'applicazione multi-tenant Usa pool elastico, è possibile utilizzare questo database primario e secondario di toomix funzionalità in ciascun pool. In questo modo è possibile diminuire hello impatto di un'interruzione di tooonly metà di tenant hello.

## <a name="best-practices-of-building-highly-available-service"></a>Procedure consigliate per la creazione di un servizio a disponibilità elevata

un servizio a disponibilità elevata che utilizza i clienti di SQL Azure database hello toobuild deve seguire queste linee guida:
- **Usare gruppi di failover**: è possibile creare uno o più gruppi di failover tra due server in aree diverse (server primario e secondario). Ogni gruppo può includere uno o più database ripristinate come un'unità nel caso in cui alcuni o tutti i database primari diventano non disponibili a causa di interruzione tooan nell'area primaria hello. gruppo di failover Hello crea geo-database secondario con hello obiettivo come hello primario del servizio stesso. Se si aggiunge che un replica geografica relazione toohello failover gruppo verificare che hello geo-secondario esistente è configurato con hello stesso come obiettivo del livello di servizio hello primario.
- **Utilizzare il listener di lettura / scrittura per carico di lavoro OLTP**: quando si esegue l'utilizzo di operazioni OLTP  **&lt;failover-group-name&gt;. database.windows.net** come URL del server hello e connessioni hello sarà toohello automaticamente diretto primario. Questo URL non verrà modificato dopo il failover hello.  
Nota hello failover comporta l'aggiornamento di hello record DNS in modo che le connessioni client hello sia reindirizzato toohello nuova primaria solo quando il client di hello cache DNS viene aggiornata.
- **Utilizzare i listener di sola lettura per il carico di lavoro di sola lettura**: se sono isolata logicamente sola lettura del carico di lavoro toocertain tolleranza d'errore obsolescenza dei dati, è possibile utilizzare i database secondari hello in un'applicazione hello. Per utilizzano le sessioni di sola lettura  **&lt;failover-group-name&gt;. secondary.database.windows.net** come URL del server hello e connessione hello saranno automaticamente diretto toohello secondario. È consigliabile anche indicare la finalità di lettura nella stringa di connessione usando **ApplicationIntent=ReadOnly**. 
- **Prevedere un calo delle prestazioni**: decisione di failover SQL è indipendente dalla parte rimanente di hello di un'applicazione hello o altri servizi utilizzati. un'applicazione Hello potrebbe essere "mixed" con alcuni componenti in un'area e alcuni in un altro. riduzione delle hello tooavoid, verificare la distribuzione di applicazioni ridondanti di hello nell'area di ripristino di emergenza hello e attenersi alle linee guida hello in questo articolo.  
Un'applicazione hello nota nell'area di ripristino di emergenza hello è toouse una stringa di connessione diversi.  
- **Preparazione per la perdita di dati**: se viene rilevata un'interruzione, SQL attiva automaticamente il failover di lettura / scrittura se è migliore di conoscendo zero toohello perdita di dati. In caso contrario, è in attesa per il periodo di hello specificata **GracePeriodWithDataLossHours**. Se è stato specificato **GracePeriodWithDataLossHours**, prepararsi a una perdita di dati. Durante le interruzioni del servizio, generalmente Azure predilige la disponibilità. Se la perdita di dati non sono consentiti, assicurarsi che tooset **GracePeriodWithDataLossHours** numero sufficientemente elevato tooa, ad esempio di 24 ore. 


## <a name="upgrading-or-downgrading-a-primary-database"></a>Aggiornamento o downgrade di un database primario
È possibile aggiornare o effettuare il downgrade di un livello di prestazioni diverse tooa database primario (all'interno di hello stesso servizio di livello) senza disconnettere i database secondari. Durante l'aggiornamento, è consigliabile aggiornare prima i database secondari hello e quindi aggiornare hello primario. La riduzione, invertire l'ordine di hello: effettuare il downgrade hello primario prima e quindi effettuare il downgrade hello secondario. Quando si aggiorna o effettuare il downgrade a livello di servizio diversi tooa hello viene applicata questa raccomandazione. 

> [!NOTE]
> Se il database secondario è stato creato come parte della configurazione del gruppo di hello failover non è consigliato toodowngrade database secondario di hello. Si tratta di tooensure del livello dati dispone di sufficiente capacità tooprocess normale carico di lavoro dopo l'attivazione di failover. 
>

## <a name="preventing-hello-loss-of-critical-data"></a>Impedire la perdita di hello di dati critici
A causa di una latenza elevata toohello delle reti WAN, copia continua viene usato un meccanismo di replica asincrona. La replica asincrona rende inevitabile una perdita parziale dei dati nel caso si verifichi un problema. Tuttavia, alcune applicazione potrebbero non essere soggette alla perdita dei dati. tooprotect questi aggiornamenti critici, uno sviluppatore di applicazioni possono chiamare hello [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx) procedure di sistema subito dopo il commit delle transazioni hello. La chiamata **sp_wait_for_database_copy_sync** hello blocchi thread chiamante finché non hello ultimo commit della transazione è stato trasmesso toohello database secondario. Tuttavia, non si attende per hello trasmesso transazioni toobe riprodotti e commit in hello secondario. **sp_wait_for_database_copy_sync** tooa con ambito collegamento di copia continua specifico. Qualsiasi utente con il database primario toohello hello connessione diritti può chiamare questa procedura.

> [!NOTE]
> **sp_wait_for_database_copy_sync** impedirà la perdita di dati dopo il failover, ma non garantirà la sincronizzazione completa per l'accesso in lettura. Hello ritardo causato da un **sp_wait_for_database_copy_sync** chiamata di routine può essere significativo e dipende dalla dimensione hello hello del log delle transazioni in fase di hello della chiamata di hello. 
> 

## <a name="programmatically-managing-failover-groups-and-active-geo-replication"></a>Gestione a livello di codice dei gruppi di failover e della replica geografica attiva
Come descritto in precedenza, i gruppi con failover automatico (in anteprima) e attiva la replica geografica può essere gestita a livello di codice con Azure PowerShell e hello API REST. Hello le tabelle seguenti vengono descritti i set di hello di comandi disponibili.

**API di gestione risorse di Azure e la sicurezza basata sui ruoli**: replica geografica attiva include un set di API di gestione risorse di Azure per la gestione, tra cui hello [API REST di Azure SQL Database](https://docs.microsoft.com/rest/api/sql/) e [Azure I cmdlet di PowerShell](https://docs.microsoft.com/powershell/azure/overview). Queste API richiedono l'uso di hello di gruppi di risorse e supportano la sicurezza basata sui ruoli (RBAC). Per ulteriori informazioni su come tooimplement accedere ai ruoli, vedere [gestire il controllo di accesso](../active-directory/role-based-access-control-what-is.md).

> [!NOTE]
> Molte nuove funzionalità della replica geografica attiva sono supportate solo con [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) e in particolare con le [API REST SQL di Azure](https://msdn.microsoft.com/library/azure/mt163571.aspx) e con i [cmdlet di PowerShell per il database SQL di Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx). Hello [API REST (classica)](https://msdn.microsoft.com/library/azure/dn505719.aspx) e [cmdlet del Database di SQL Azure (versione classica)](https://msdn.microsoft.com/library/azure/dn546723.aspx) sono supportate per compatibilità con le versioni precedenti, pertanto l'uso di hello API basate su Gestione risorse di Azure sono consigliate. 
> 

## <a name="manage-sql-database-failover-using-using-transact-sql"></a>Gestire SQL database failover utilizzando Transact-SQL

| Comando | Descrizione |
| --- | --- |
| [ALTER DATABASE (database SQL di Azure)](https://msdn.microsoft.com/library/mt574871.aspx) |Utilizzare Aggiungi secondario ON SERVER argomento toocreate un database secondario per un database esistente e avvia la replica dei dati |
| [ALTER DATABASE (database SQL di Azure)](https://msdn.microsoft.com/library/mt574871.aspx) |Utilizzare il FAILOVER o FORCE_FAILOVER_ALLOW_DATA_LOSS tooswitch failover primario tooinitiate toobe database secondario |
| [ALTER DATABASE (database SQL di Azure)](https://msdn.microsoft.com/library/mt574871.aspx) |Utilizzare tooterminate rimuovere ON SERVER secondario una replica dei dati tra un Database SQL e il database secondario specificato hello. |
| [sys.geo_replication_links (database SQL di Azure)](https://msdn.microsoft.com/library/mt575501.aspx) |Restituisce informazioni su tutti i collegamenti di replica esistente per ogni database nel server logico di Database SQL di Azure hello. |
| [sys.dm_geo_replication_link_status (database SQL di Azure)](https://msdn.microsoft.com/library/mt575504.aspx) |Ottiene hello ora dell'ultima replica, l'ultimo intervallo di replica e altre informazioni sul collegamento di replica hello per un determinato database SQL. |
| [sys.dm_operation_status (database SQL di Azure)](https://msdn.microsoft.com/library/dn270022.aspx) |Mostra lo stato di hello per tutte le operazioni di database, incluso lo stato di hello hello dei collegamenti di replica. |
| [sp_wait_for_database_copy_sync (database SQL di Azure)](https://msdn.microsoft.com/library/dn467644.aspx) |causa toowait applicazione hello fino a quando tutte le transazioni completate vengono replicate e riconosciute dal database secondario attivo hello. |
|  | |

## <a name="manage-sql-database-failover-using-using-powershell"></a>Gestire SQL database failover utilizzando PowerShell

| Cmdlet | Descrizione |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Ottiene uno o più database. |
| [New-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary) |Crea un database secondario per un database esistente e avvia la replica dei dati. |
| [Set-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary) |Attiva un failover primario tooinitiate toobe di database secondario. |
| [Remove-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) |Termina la replica dei dati tra un Database SQL e il database secondario specificato hello. |
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) |Ottiene i collegamenti di replica geografica hello tra un Database SQL di Azure e un gruppo di risorse o SQL Server. |
| [New-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Questo comando crea un gruppo di failover e lo registra nei server primario e secondario|
| [Remove-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/remove-azurermsqldatabasefailovergroup) | Rimuove il gruppo di failover di hello dal server hello ed Elimina tutti i database secondari inclusi hello gruppo |
| [Get-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/get-azurermsqldatabasefailovergroup) | Configurazione del gruppo recupera hello failover |
| [Set-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Modifica configurazione hello hello del gruppo del failover |
| [Switch-AzureRMSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/switch-azurermsqldatabasefailovergroup) | Attiva il failover del server secondario toohello hello failover gruppo |
|  | |

> [!IMPORTANT]
> Per gli script di esempio, vedere [Configurare la replica geografica attiva per un database SQL di Azure singolo usando PowerShell](scripts/sql-database-setup-geodr-and-failover-database-powershell.md), [Configurare la replica geografica attiva per un database SQL di Azure in pool con PowerShell](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md) e [Configure and failover a failover group for a single database (preview) (Configurare un gruppo di failover ed eseguirne il failover per un singolo database (anteprima))] (scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md.
>

## <a name="manage-sql-database-failover-using-hello-rest-api"></a>Failover del database SQL tramite hello API REST di gestione
| API | Descrizione |
| --- | --- |
| [Creare o aggiornare database (createMode=Restore)](/rest/api/sql/Databases/CreateOrUpdate) |Crea, aggiorna o ripristina un database primario o secondario. |
| [Get Create or Update Database Status](/rest/api/sql/Databases/CreateOrUpdate) |Restituisce lo stato di hello durante un'operazione di creazione. |
| [Impostazione del database secondario come primario (failover pianificato)](https://docs.microsoft.com/rest/api/sql/replicationlinkss#ReplicationLinks_Failover) |Imposta il database di replica è primario eseguendo il failover dal database di replica primaria corrente hello. |
| [Set Secondary Database as Primary (Unplanned Failover)](https://docs.microsoft.com/rest/api/sql/replicationlinks#ReplicationLinks_FailoverAllowDataLoss) |Imposta il database di replica è primario eseguendo il failover dal database di replica primaria corrente hello. Questa operazione potrebbe comportare la perdita di dati. |
| [Get Replication Link](/rest/api/sql/replicationlinks/get) |Ottiene tutti i collegamenti di replica specifici per un database SQL specificato in una relazione di replica geografica. Recupera le informazioni di hello visibili nella vista del catalogo sys.geo_replication_links hello. |
| [Replication Links - List By Database](/rest/api/sql/replicationlinks/listbydatabase) | Ottiene tutti i collegamenti di replica per un database SQL specificato in una relazione di replica geografica. Recupera le informazioni di hello visibili nella vista del catalogo sys.geo_replication_links hello. |
| [Delete Replication Link](/rest/api/sql/databases/delete) | Elimina un collegamento alla replica del database. Non può essere eseguito durante il failover. |
| [Create or Update Failover Group]/rest/api/sql/failovergroups/createorupdate) | Crea o aggiorna un gruppo di failover. |
| [Delete Failover Group](/rest/api/sql/failovergroups/delete) | Rimuove il gruppo di failover di hello server hello |
| [Failover (Planned)](/rest/api/sql/failovergroups/failover) | Viene eseguito il failover dal server di toothis server primario corrente hello. |
| [Force Failover Allow Data Loss](/rest/api/sql/failovergroups/forcefailoverallowdataloss) |ails failover dal server di toothis server primario corrente hello. Questa operazione potrebbe comportare la perdita di dati. |
| [Get Failover Group](/rest/api/sql/failovergroups/get) | Crea un gruppo di failover. |
| [List Failover Groups By Server](/rest/api/sql/failovergroups/listbyserver) | Elenca i gruppi di failover hello in un server. |
| [Update Failover Group](/rest/api/sql/failovergroups/update) | Aggiorna un gruppo di failover. |
|  | |

## <a name="next-steps"></a>Passaggi successivi
* Per script di esempio, vedere:
   - [Configurare un database singolo ed eseguirne il failover usando la replica geografica attiva](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
   - [Configurare un database in pool ed eseguirne il failover usando la replica geografica attiva](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md)
   - [Configure and failover a failover group for a single database (preview)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md) (Configurare ed eseguire il failover di un gruppo di failover per un singolo database (anteprima))
* Per la panoramica e gli scenari della continuità aziendale, vedere [Continuità aziendale del database SQL di Azure](sql-database-business-continuity.md)
* toolearn sui backup di Database di SQL Azure automatizzati, vedere [backup automatici di Database SQL](sql-database-automated-backups.md).
* toolearn sull'utilizzo di backup automatico per il ripristino, vedere [ripristinare un database dai backup avviate dal servizio hello](sql-database-recovery-using-backups.md).
* toolearn sui requisiti di autenticazione per un nuovo server primario e il database, vedere [la protezione del Database di SQL dopo il ripristino di emergenza](sql-database-geo-replication-security-config.md).

