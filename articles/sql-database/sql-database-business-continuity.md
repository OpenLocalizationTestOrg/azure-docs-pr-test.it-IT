---
title: "continuità aziendale aaaCloud - ripristino del database - Database SQL | Documenti Microsoft"
description: "Informazioni su come il database SQL di Azure supporta la continuità aziendale cloud e il ripristino del database e consente di mantenere le applicazioni cloud cruciali in esecuzione."
keywords: "continuità aziendale, continuità aziendale cloud, ripristino di emergenza del database, ripristino del database"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 18e5d3f1-bfe5-4089-b6fd-76988ab29822
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/15/2017
ms.author: sashan
ms.openlocfilehash: c9a6ff86fbbc04ce839a4fca79594b573b71644c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-business-continuity-with-azure-sql-database"></a>Panoramica della continuità aziendale del database SQL di Azure

Questa panoramica descrive le funzionalità di hello fornito da un Database SQL di Azure per la continuità aziendale e ripristino di emergenza. Informazioni sulle opzioni, indicazioni e le esercitazioni per il ripristino da eventi di arresto improvviso che potrebbero provocare la perdita di dati o il database e dell'applicazione toobecome è disponibile. Informazioni su quali toodo quando un utente o un'applicazione di errore interessa l'integrità dei dati, un'area di Azure dispone di un'interruzione o l'applicazione richiede attività di manutenzione.

## <a name="sql-database-features-that-you-can-use-tooprovide-business-continuity"></a>Funzionalità di Database SQL che è possibile usare la continuità aziendale tooprovide

Il database SQL offre diverse funzionalità di continuità aziendale, inclusi i backup automatici e la replica facoltativa del database. Ogni funzionalità presenta caratteristiche diverse in termini di tempo di recupero stimato (ERT) e di potenziale perdita di dati per le transazioni recenti. Dopo aver compreso le opzioni disponibili, è possibile scegliere una di esse o, nella maggior parte dei casi, usarle in modo combinato per i diversi scenari. Quando si sviluppa il piano di continuità aziendale, è necessario toounderstand hello massimo accettabile tempo prima che un'applicazione hello completamente ripristinato dopo evento di arresto improvviso hello - questo è l'obiettivo del tempo di ripristino (RTO). È inoltre necessario toounderstand quantità massima di hello di un'applicazione hello aggiornamenti (intervallo di tempo) dati recenti è in grado di tollerare perdere durante il recupero dopo l'evento di arresto improvviso hello - questo è l'obiettivo del punto di ripristino (RPO).

Hello seguente tabella confronta hello ERT e RPO per scenari più comuni di hello tre.

| Funzionalità | Livello Basic | Livello Standard | Livello Premium |
| --- | --- | --- | --- |
| Ripristino temporizzato dal backup |Qualsiasi punto di ripristino entro 7 giorni |Qualsiasi punto di ripristino entro 35 giorni |Qualsiasi punto di ripristino entro 35 giorni |
| Ripristino geografico dai backup con replica geografica |ERT < 12 ore, RPO < 1 ora |ERT < 12 ore, RPO < 1 ora |ERT < 12 ore, RPO < 1 ora |
| Ripristino dall'insieme di credenziali di Backup di Azure |ERT < 12 ore, RPO < 1 sett |ERT < 12 ore, RPO < 1 sett |ERT < 12 ore, RPO < 1 sett |
| Replica geografica attiva |ERT < 30 sec, RPO < 5 sec |ERT < 30 sec, RPO < 5 sec |ERT < 30 sec, RPO < 5 sec |

### <a name="use-database-backups-toorecover-a-database"></a>Utilizzare i backup di database toorecover un database

Database SQL esegue automaticamente una combinazione di backup completi del database ogni settimana, ogni ora backup differenziale del database e transazioni i backup del log ogni 5-dieci minuti tooprotect azienda dalla perdita di dati. Questi backup vengono archiviati nel servizio di archiviazione con ridondanza geografica per 35 giorni per i database nei livelli di servizio Standard e Premium hello e 7 giorni per i database nel livello di servizio Basic hello. Per altre informazioni, vedere [livelli di servizio](sql-database-service-tiers.md). Se il periodo di memorizzazione hello per il livello di servizio non soddisfa i requisiti aziendali, è possibile aumentare il periodo di memorizzazione hello da [modifica il livello di servizio hello](sql-database-service-tiers.md). Hello backup completi e differenziali del database vengono inoltre replicato tooa [centro dati associato](../best-practices-availability-paired-regions.md) per la protezione da un'interruzione del centro dati. Per altre informazioni, vedere [backup automatici del database SQL](sql-database-automated-backups.md).

Se il periodo di memorizzazione predefinite di hello non sono sufficiente per l'applicazione, è possibile estenderlo configurando un criterio di conservazione a lungo termine di database. Per altre informazioni, vedere [Long-term retention](sql-database-long-term-retention.md) (Conservazione a lungo termine).

È possibile utilizzare questi toorecover backup automatica del database un database da vari eventi di arresto improvviso, sia all'interno del centro dati e tooanother data center. Utilizzo dei backup automatica del database, hello stimato momento del ripristino dipende da diversi fattori, incluso il numero totale di hello di ripristinare in hello stesso database area di hello stesso tempo, hello dimensioni del database, dimensioni del log delle transazioni, hello e larghezza di banda di rete. tempo di recupero Hello è in genere meno di 12 ore. Quando si ripristina l'area dati tooanother, hello perdita di dati è ora too1 limitato per l'archiviazione con ridondanza geografica hello del backup differenziale del database ogni ora.

> [!IMPORTANT]
> toorecover utilizzando backup automatici, è necessario essere un membro del ruolo di collaboratore di SQL Server hello o il proprietario della sottoscrizione hello: vedere [RBAC: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md). È possibile ripristinare utilizzando hello portale di Azure, PowerShell o hello API REST. Non è possibile usare Transact-SQL.
>

Usare i backup automatici come meccanismo di continuità e ripristino aziendale, se l'applicazione:

* Non è considerata cruciale.
* Non ha un contratto di servizio vincolante: un tempo di inattività di 24 o più ore non comporta alcuna responsabilità finanziaria.
* Ha una bassa frequenza di modifica dei dati (basse transazioni all'ora) e la perdita di tooan una perdita di dati accettabile è un'ora di modifica.
* Dipende dal costo.

Se è necessario un ripristino più veloce, usare la [Replica geografica attiva](sql-database-geo-replication-overview.md) (più avanti). Se è necessario toobe toorecover in grado di dati di un periodo antecedente a 35 giorni, utilizzare [conservazione dei backup a lungo termine](sql-database-long-term-retention.md). 

### <a name="use-active-geo-replication-and-auto-failover-groups-in-preview-tooreduce-recovery-time-and-limit-data-loss-associated-with-a-recovery"></a>Utilizzare attivo con failover automatico e la replica geografica gruppi (in anteprima) tooreduce ripristino ora e limitare la perdita di dati associata a un ripristino

Inoltre toousing i backup di database per il ripristino del database se si verifica un'interruzione di business, è possibile utilizzare [replica geografica attiva](sql-database-geo-replication-overview.md) tooconfigure toohave un database di toofour database secondari leggibili in aree hello del scelta. Questi database secondari vengono mantenuti sincronizzati con il database primario di hello utilizzando un meccanismo di replica asincrona. Questa funzionalità è utilizzata tooprotect interruzioni delle attività aziendali se si verifica un'interruzione del centro dati o durante un aggiornamento dell'applicazione. Replica geografica attiva può essere anche usato tooprovide migliori le prestazioni delle query per gli utenti toogeographically in diverse località geografiche di query di sola lettura.

tooenable automatico e il failover trasparente è necessario organizzare i database di replica geografica in gruppi utilizzando hello [con failover automatico gruppo](sql-database-geo-replication-overview.md) funzionalità del Database SQL (in anteprima).

Se il database primario hello passa alla modalità offline in modo imprevisto o se è necessario tootake non in linea per attività di manutenzione, è possibile rapidamente promuovere un database primario hello toobecome secondario (detto anche un failover) e configurare primario toohello alzate di livello tooconnect di applicazioni. Se l'applicazione si connette database toohello tramite hello listener del gruppo di failover, è necessario toochange configurazione di stringa di connessione SQL a hello dopo il failover. Con un failover pianificato, non si verificano perdite di dati. Con un failover non pianificato, potrebbero essere presenti alcune piccole quantità di perdita di dati per le transazioni molto recente a causa di natura toohello di replica asincrona. Se si utilizzano i gruppi con failover automatico (in anteprima), è possibile personalizzare hello failover criteri toominimize hello potenziale perdita di dati. Dopo un failover, è possibile eseguire il failback successive - secondo piano tooa o quando hello del data center torna online. In tutti i casi, gli utenti verificano una piccola quantità di tempo di inattività e necessario tooreconnect.

> [!IMPORTANT]
> toouse la replica geografica attiva e gruppi con failover automatico (in anteprima), è necessario essere proprietario della sottoscrizione hello o disporre di autorizzazioni amministrative in SQL Server. È possibile configurare il failover utilizzando hello portale di Azure PowerShell o hello API REST di utilizzo delle autorizzazioni di sottoscrizione di Azure o tramite Transact-SQL con autorizzazioni di SQL Server.
> 

Usare la replica geografica attiva e i gruppi con failover automatico (in anteprima) se l'applicazione soddisfa qualcuno dei criteri seguenti:

* È considerata cruciale.
* Ha un contratto di servizio che non consente più di 24 ore di inattività.
* Il tempo di inattività può implicare responsabilità finanziaria.
* Ha una frequenza elevata di modifica dei dati e la perdita di un'ora di dati non è accettabile.
* Hello costi aggiuntivi per la replica geografica attiva sono inferiori a responsabilità finanziaria potenziali hello e perdite di business.

>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-protecting-important-DBs-from-regional-disasters-is-easy/player]
>

## <a name="recover-a-database-after-a-user-or-application-error"></a>Ripristinare un database in seguito a errore di un'applicazione o un utente
* Nessuno è perfetto! Un utente potrebbe accidentalmente eliminare alcuni dati, una tabella importante o addirittura un intero database. In alternativa, un'applicazione potrebbe sovrascrivere accidentalmente dati validi con i dati non validi a causa di errore di applicazione tooan.

In questo scenario, ecco sono le opzioni di ripristino.

### <a name="perform-a-point-in-time-restore"></a>Eseguire un ripristino temporizzato
È possibile utilizzare toorecover backup automatizzato hello una copia di tooa il database noti buon punto nel tempo, condizione che ora è nel periodo di memorizzazione del database hello. Dopo il ripristino di database hello, è possibile sostituire database originale hello con il database ripristinato hello o copiare i dati di hello necessita da dati hello ripristinato nel database originale hello. Se il database di hello utilizza la replica geografica attiva, è consigliabile la copia dei dati di hello richiesto dalla copia hello ripristinato nel database originale hello. Se si sostituisce database originale hello con database hello ripristinato, è necessario tooreconfigure e risincronizzare la replica geografica attiva (che può richiedere molto tempo per un database di grandi dimensioni).

Per ulteriori informazioni e per i passaggi dettagliati per il ripristino di un punto di tooa database in esecuzione utilizzando hello portale di Azure o tramite PowerShell, vedere [in fase di punto di ripristino](sql-database-recovery-using-backups.md#point-in-time-restore). Non è possibile eseguire il ripristino tramite Transact-SQL.

### <a name="restore-a-deleted-database"></a>Ripristino di un database eliminato
Se hello database viene eliminato ma non è stata eliminata server logico hello, è possibile ripristinare i punti di toohello database hello eliminato in corrispondenza del quale è stato eliminato. Ciò consente di ripristinare un toohello di backup del database stesso server SQL logico da cui è stato eliminato. È possibile ripristinarla utilizzando nome originale hello o fornire un nuovo nome o un database ripristinato hello.

Per ulteriori informazioni e per i passaggi dettagliati per il ripristino di un database eliminato utilizzando hello portale di Azure o tramite PowerShell, vedere [ripristinare un database eliminato](sql-database-recovery-using-backups.md#deleted-database-restore). Non è possibile eseguire il recupero tramite Transact-SQL.

> [!IMPORTANT]
> Se il server logico hello viene eliminato, è possibile ripristinare un database eliminato.
>
>

### <a name="restore-from-azure-backup-vault"></a>Ripristino dall'insieme di credenziali di Backup di Azure
Se si è verificato la perdita di dati hello esterno hello periodo di memorizzazione corrente per i backup automatici e il database è configurato per la conservazione a lungo termine, è possibile ripristinare da un backup nel nuovo database di archivio di Backup di Azure tooa settimana. A questo punto, è possibile sostituire database originale hello con il database ripristinato hello o copiare i dati di hello necessita dal database di hello ripristinato nel database originale hello. Se è necessario tooretrieve una versione precedente dell'aggiornamento del database precedente tooa principale dell'applicazione, soddisfare una richiesta da controllori o un ordine valido, che è possibile creare un database utilizzando un backup completo, salvato in hello insieme di credenziali di Azure Backup.  Per altre informazioni, vedere [Long-term retention](sql-database-long-term-retention.md) (Conservazione a lungo termine).

## <a name="recover-a-database-tooanother-region-from-an-azure-regional-data-center-outage"></a>Ripristinare un'area tooanother database da un'interruzione del centro dati regionale di Azure
<!-- Explain this scenario -->

Anche se raramente, un data center di Azure può subire un'interruzione del servizio. Quando si verifica un'interruzione, viene generata un'interruzione delle attività che potrebbe durare solo pochi minuti oppure ore.

* Un'opzione è toowait per il toocome database online quando si trova sull'interruzione di hello data center. Questo procedimento funziona per le applicazioni che possono permettersi di database non in linea di toohave hello. Ad esempio, un progetto di sviluppo o di una versione di valutazione gratuita non è necessario toowork su costantemente. Quando un data center dispone di un'interruzione del servizio, non si conosce interruzione hello potrebbe durata, pertanto questa opzione funziona solo se il database non è necessario per un periodo di tempo.
* Un'altra opzione è tooeither fail sull'area dati tooanother se si utilizza la replica geografica attiva o hello ripristinare un database tramite backup di database archiviazione con ridondanza geografica (ripristino a livello geografico). Il failover richiede solo pochi secondi mentre il ripristino del database da backup richiede ore.

Quando si utilizza l'azione, il tempo impiegato per toorecover, e quanto si verifica la perdita di dati dipende da come si decide di toouse queste funzionalità di continuità aziendale nell'applicazione. In effetti, è possibile scegliere toouse una combinazione di backup del database e di replica geografica attiva varia a seconda dei requisiti dell'applicazione. Per una descrizione delle considerazioni sulla progettazione di applicazioni per database autonomi e pool elastici tramite queste funzioni di continuità aziendale, vedere [Progettare un'applicazione per il ripristino di emergenza cloud](sql-database-designing-cloud-solutions-for-disaster-recovery.md) e [Strategie di ripristino di emergenza per applicazioni che usano il pool elastico del database SQL](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

Hello nelle sezioni seguenti forniscono una panoramica di hello passaggi toorecover utilizzando backup di database o la replica geografica attiva. Per istruzioni dettagliate, inclusa la pianificazione di requisiti, i passaggi di ripristino post e informazioni su come toosimulate un tooperform interruzione un ripristino di emergenza eseguire il drill-, vedere [ripristinare un Database SQL di un'interruzione](sql-database-disaster-recovery.md).

### <a name="prepare-for-an-outage"></a>Prepararsi a un'interruzione del servizio
Indipendentemente dalla funzionalità di continuità aziendale hello che è utilizzare, è necessario:

* Identificare e preparare il server di destinazione hello, incluse le regole del firewall a livello di server, gli account di accesso e le autorizzazioni a livello di database master.
* Determinare come tooredirect client e server nuovo toohello di applicazioni client
* Documentare altre dipendenze, ad esempio impostazioni di controllo e avvisi

Se non ci si prepara adeguatamente al ripristino, riportare online le applicazioni dopo un failover o un ripristino del database richiederà ulteriore tempo e probabilmente la risoluzione di problemi aggiuntivi in un momento di stress: una combinazione da evitare.

### <a name="fail-over-tooa-geo-replicated-secondary-database"></a>Eseguire il failover il database secondario di replica geografica tooa
Se si usa la replica geografica attiva e i gruppi con failover automatico (in anteprima) come meccanismo di ripristino, è possibile configurare i criteri di failover automatico o usare il [failover manuale](sql-database-disaster-recovery.md#fail-over-to-geo-replicated-secondary-database). Una volta avviata, hello failover cause hello secondario toobecome hello nuovo primario e pronto toorecord nuove transazioni e rispondere tooqueries - con perdita di dati minima per i dati di hello non ancora replicate. Per informazioni sulla progettazione di processo di failover di hello, vedere [progettare un'applicazione per il ripristino di emergenza cloud](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

> [!NOTE]
> Quando torna online centro dati hello primari precedente hello automaticamente riconnettersi toohello nuovo database primario e diventano database secondari. Se è necessario l'area di toorelocate hello toohello indietro primaria originale, è possibile avviare manualmente un failover pianificato (failback). 
> 

### <a name="perform-a-geo-restore"></a>Eseguire un ripristino geografico
Se si usano backup automatici con la replica dell'archiviazione con ridondanza geografica come meccanismo di ripristino, [avviare il ripristino del database tramite ripristino geografico](sql-database-disaster-recovery.md#recover-using-geo-restore). Ripristino in genere avviene all'interno di 12 ore, con perdita di dati di backup ora tooone era al momento hello ultimo backup differenziale orario con eseguito e replicato. Fino a quando non viene completato il ripristino di hello, database di hello è Impossibile toorecord tutte le transazioni o risposta tooany query. Mentre ciò consente di ripristinare un database toohello ultimo disponibili punto nel tempo, ripristino hello geografica secondario tooany punto nel tempo non è attualmente supportato.

> [!NOTE]
> Se centro dati hello ritorna online prima di passare all'applicazione nel database ripristinato toohello, è possibile annullare il ripristino di hello.  
>
>

### <a name="perform-post-failover--recovery-tasks"></a>Eseguire attività successive al filover/ripristino
Dopo il ripristino da uno dei due meccanismi di ripristino, è necessario eseguire hello seguenti attività aggiuntive prima che gli utenti e applicazioni di eseguire il backup e in esecuzione:

* Reindirizzare i client e server nuovo toohello di applicazioni client e il database ripristinato
* Verificare le regole del firewall a livello di server appropriati sono disponibili per gli utenti tooconnect (o utilizzare [firewall a livello di database](sql-database-firewall-configure.md#creating-and-managing-firewall-rules))
* Verificare che siano presenti gli account di accesso appropriato e le autorizzazioni a livello di database master o usare gli [utenti contenuti](https://msdn.microsoft.com/library/ff929188.aspx)
* Configurare il controllo in base alle proprie esigenze.
* Configurare gli avvisi in base alle proprie esigenze.

## <a name="upgrade-an-application-with-minimal-downtime"></a>Aggiornare un'applicazione con tempo di inattività minimo
A volte un'applicazione deve essere portata offline per ragioni di manutenzione pianificata, ad esempio un aggiornamento dell'applicazione. [Gestire gli aggiornamenti dell'applicazione](sql-database-manage-application-rolling-upgrade.md) viene descritto come tooenable di replica geografica attiva toouse eseguire aggiornamenti di tempo di inattività di toominimize applicazione cloud durante l'aggiornamento e fornire un percorso di recupero in caso di errore. 

## <a name="next-steps"></a>Passaggi successivi
Per una descrizione delle considerazioni sulla progettazione di applicazioni per database autonomi e pool elastici, vedere [Progettare un'applicazione per il ripristino di emergenza cloud](sql-database-designing-cloud-solutions-for-disaster-recovery.md) e [Strategie di ripristino di emergenza per applicazioni che usano il pool elastico del database SQL](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
