---
title: "aaaWhat è servizio di Database SQL di Azure hello? | Microsoft Docs"
description: "Ottenere un Database di tooSQL Introduzione: dettagli tecnici e le funzionalità di Microsoft relazionale del database di sistema di gestione (RDBMS) nel cloud hello."
keywords: "Introduzione toosql, toosql introduzione, qual è il database sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cgronlun
ms.assetid: c561f600-a292-4e3b-b1d4-8ab89b81db48
ms.service: sql-database
ms.custom: overview
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: 24ca383ad7e140133d19debc8899f172ee4aa424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-sql-database-service"></a>Che cos'è il servizio di Database SQL di Azure hello? 

Il database SQL è un servizio di database relazionale generico in Microsoft Azure che supporta strutture come dati relazionali, JSON, dati spaziali e XML. Questo servizio offre [prestazioni con scalabilità dinamica](sql-database-service-tiers.md) e opzioni come gli [indici columnstore](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview) per funzionalità di analisi e report avanzatissime e [OLTP in memoria](sql-database-in-memory.md) per l'elaborazione XTP (Extreme Transaction Processing). Microsoft gestisce tutte le operazioni di aggiornamento di base di codice SQL hello facilmente e l'applicazione di patch ed estrae tutti i management di hello infrastruttura sottostante. 

Database SQL condivide la codebase con hello [il motore di database di Microsoft SQL Server](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation). Con cloud prima strategia Microsoft, le funzionalità più recenti di hello di SQL Server sono rilasciati tooSQL primo Database e quindi tooSQL Server stesso. Questo approccio offre hello più recenti funzionalità di SQL Server con alcun overhead per l'applicazione di patch o l'aggiornamento e con queste nuove funzionalità di sottoporre a test in milioni di database. Per informazioni sulle nuove funzionalità annunciate, vedere:

- **[Guida di orientamento per Azure per il Database SQL](https://azure.microsoft.com/roadmap/?category=databases)**: toofind un luogo le novità e sviluppi futuri successivo. 
- **[Blog di database SQL di Azure](https://azure.microsoft.com/blog/topics/database)**: raccoglitore dei post dei membri del team di prodotto SQL Server sulle novità e le funzionalità di database SQL. 

Il database SQL offre prestazioni prevedibili a più livelli di servizio garantendo scalabilità dinamica senza tempi di inattività, ottimizzazione intelligente incorporata, scalabilità e disponibilità globali e opzioni di sicurezza avanzate, il tutto con esigenze di amministrazione quasi nulle. Queste funzionalità consentono di toofocus sullo sviluppo rapido di app e accelerare il tempo toomarket, invece di allocare il tempo e risorse toomanaging le macchine virtuali e l'infrastruttura. Database SQL di servizio è attualmente in 38 dati Hello coinvolge HelloWorld, con più data center torna online regolarmente, che consentono di toorun del database in un data center più vicino.

> [!NOTE]
> Vedere [Centro protezione di Azure](https://azure.microsoft.com/support/trust-center/security/) per informazioni sulla sicurezza della piattaforma Azure.
>

## <a name="scalable-performance-and-pools"></a>Prestazioni e pool scalabili

Con database SQL, ogni database è isolato dagli altri e portabile e a ognuno viene assegnato un [livello di servizio](sql-database-service-tiers.md) proprio con un livello di prestazioni garantito. Database SQL fornisce diversi livelli di prestazioni per esigenze diverse e consente ai database hello in pool toomaximize toobe l'uso delle risorse e risparmiare denaro.

### <a name="adjust-performance-and-scale-without-downtime"></a>Regolare le prestazioni e scalabilità senza tempi di inattività

Database SQL offre quattro livelli di servizio carichi di lavoro database leggero tooheavyweight toosupport: Basic, Standard, Premium e RS Premium. È possibile compilare la prima app in un database di piccole dimensioni, singolo a basso costo al mese e quindi modificare il livello di servizio manualmente o a livello di codice le esigenze di hello toomeet ora della soluzione. È possibile regolare le prestazioni senza tempi di inattività tooyour app tooyour clienti. Consente la scalabilità dinamica tootransparently il database rispondere toorapidly la modifica di requisiti di risorse e attiva tooonly si paga per risorse hello che è necessario quando necessario.

   ![scalabilità](./media/sql-database-what-is-a-dtu/single_db_dtus.png)

### <a name="elastic-pools-toomaximize-resource-utilization"></a>Utilizzo delle risorse toomaximize pool elastici

Per molte aziende e applicazioni, da toocreate in grado di singoli database e comporre prestazioni verso l'alto o verso il basso su richiesta è sufficiente, specialmente se i modelli di utilizzo sono relativamente prevedibili. Ma se si dispone di modelli di utilizzo imprevisti, può risultare toomanage rigido costi e il modello aziendale. [Pool elastici](sql-database-elastic-pool.md) è toosolve progettato il problema. il concetto di Hello è semplice. È possibile allocare pool tooa risorse di prestazioni, anziché un singolo database e pagare per le risorse di hello collettivi delle prestazioni del pool di hello anziché per le prestazioni del database singolo. 

   ![pool elastici](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

Il pool elastico, non è necessario toofocus nella composizione delle prestazioni del database su e giù man mano che cambia la richiesta di risorse. Hello in pool di database utilizzano risorse hello per le prestazioni del pool elastico hello in base alle esigenze. Pool di database utilizzano ma non superano i limiti di hello del pool di hello, pertanto il costo rimane stimabile anche se non l'utilizzo del database singoli. In particolare, è possibile [aggiungere e rimuovere il pool di database toohello](sql-database-elastic-pool-manage-portal.md), l'app da un numero limitato di toothousands database, all'interno di un budget che è possibile controllare la scalabilità. È anche possibile minimo hello controllo e risorse massimo toodatabases disponibile in tooensure pool hello che nessun database nel pool di hello utilizza tutti hello risorse del pool e che disponga di una quantità minima garantita delle risorse da parte di ogni database nel pool. toolearn ulteriori informazioni sui modelli di progettazione per le applicazioni SaaS con i pool elastici, vedere [modelli di progettazione per le applicazioni SaaS multi-tenant con il Database SQL](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="blend-single-databases-with-pooled-databases"></a>Unire database singoli e database nel pool

In entrambi i casi, ovvero database singoli o database nel pool, sono disponibili molte opzioni. È possibile blend singoli database con un pool elastico e modificare i livelli di servizio hello di singoli database e i pool elastici rapidamente e facilmente tooadapt tooyour situazione. Con power hello e potenzialità di Azure, è possibile e sconto altri Azure servizi con Database SQL toomeet app univoco di progettazione alle esigenze, l'unità di costo e l'efficienza delle risorse e sbloccare nuove opportunità di business.

### <a name="extensive-monitoring-and-alerting-capabilities"></a>Funzionalità complete di monitoraggio e avviso

Ma come è possibile confrontare le prestazioni relativo hello di singoli database e i pool elastici? Come è possibile sapere a destra fare clic su Arresta hello quando ci si connette su e giù? Utilizzare hello [il monitoraggio delle prestazioni predefinite](sql-database-performance.md) e [avvisi](sql-database-insights-alerts-portal.md) strumenti, in base alle valutazioni delle prestazioni hello [unità di transazione Database (Dtu) per singoli database e Dtu elastiche (Edtu) per il pool elastico](sql-database-what-is-a-dtu.md). Utilizzando questi strumenti consentono di valutare rapidamente impatto hello di ridimensionamento verso l'alto o verso il basso in base a corrente o progetto esigenze di prestazioni. Per altre informazioni, vedere [Opzioni e prestazioni disponibili in ogni livello di servizio del database SQL](sql-database-service-tiers.md) .

Database SQL può anche [generare log di metrica e diagnostica](sql-database-metrics-diag-logging.md) per facilitare il monitoraggio. È possibile configurare l'utilizzo delle risorse di Database SQL toostore, thread di lavoro e le sessioni e connettività in una di queste risorse di Azure:

- **Archiviazione di Azure**: per l'archiviazione di enormi quantità di dati di telemetria a un costo conveniente
- **Hub eventi di Azure**: per l'integrazione dei dati di telemetria di database SQL con soluzioni di monitoraggio personalizzate o pipeline attive
- **Log Analytics di Azure**: per usare una soluzione di monitoraggio incorporata con funzionalità di report, avviso e mitigazione

    ![architettura](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="availability-capabilities"></a>Funzionalità per la disponibilità

Il settore di Azure che ha una accordo sul livello di disponibilità del servizio del 99,99% [(SLA)](http://azure.microsoft.com/support/legal/sla/), fornito da una rete globale di datacenter gestiti da Microsoft, consente di mantenere l'applicazione in esecuzione 24 ore su 24, 7 giorni su 7. Il database SQL offre anche funzionalità di [continuità aziendale e scalabilità globale](sql-database-business-continuity.md) incorporate, tra le quali:

- **[Backup automatici](sql-database-automated-backups.md)**: il database SQL esegue automaticamente backup completi, differenziali e del log delle transazioni.
- **[Ripristini temporizzati in](sql-database-recovery-using-backups.md)**: il Database SQL supporta un punto di ripristino tooany nel tempo entro il periodo di conservazione dei backup automatici hello.
- **[Replica geografica attiva](sql-database-geo-replication-overview.md)**: il Database SQL consente tooconfigure backup di database secondario leggibile toofour i database in entrambi hello stesso o a livello globale distributed data center di Azure.  Ad esempio, se si dispone di un'applicazione SaaS con un database di catalogo che include un numero elevato di transazioni simultanee di sola lettura, utilizzare la replica geografica attiva tooenable globale leggere scala e rimuovere colli di bottiglia in hello primario che sono in scadenza tooread i carichi di lavoro. 
- **[Gruppi di failover](sql-database-geo-replication-overview.md)**: Database SQL consente tooenable la disponibilità elevata e bilanciamento del carico su scala globale, tra cui la replica geografica trasparente e il failover delle grandi set di database e i pool elastici. I gruppi di failover e abilita la creazione replica geografica attiva delle applicazioni SaaS distribuite a livello globale con amministrazione minimo overhead lasciando tutti hello complessi di monitoraggio, routing e failover orchestrazione tooSQL Database.

## <a name="built-in-intelligence"></a>Intelligenza incorporata

Con il Database SQL, si otterrà un intelligence incorporato che consente di ridurre notevolmente i costi di hello di esecuzione e la gestione di database e consente di ottimizzare prestazioni e sicurezza dell'applicazione. Database SQL in esecuzione milioni di clienti i carichi di lavoro 24 ore su 24, raccoglie ed elabora una notevole quantità di dati di telemetria, rispettando completamente background hello privacy dei clienti. Vari algoritmi continuamente valutare i dati di telemetria hello in modo che il servizio hello informazioni e adattarsi con l'applicazione. In base a questa analisi, il servizio di hello è dotato della prestazioni del carico di lavoro di indicazioni tooyour personalizzati specifici di miglioramento. 

### <a name="automatic-performance-tuning"></a>Ottimizzazione automatica delle prestazioni

Database SQL fornisce una visione dettagliata hello query che è necessario toomonitor. Database SQL di riceve informazioni relative ai modelli di database e consente si tooadapt il carico di lavoro tooyour dello schema del database. Il database SQL offre raccomandazioni per ottimizzare le prestazioni tramite lo strumento [Advisor per database SQL](sql-database-advisor.md), nel quale è possibile verificare le azioni di ottimizzazione e applicarle. Il monitoraggio costante dei database è tuttavia un'attività complessa e tediosa, in particolare quando sono coinvolti molti database. Gestisce un numero elevato di database potrebbe essere impossibile toodo in modo efficiente anche tutti gli strumenti disponibili e i rapporti forniti da Database SQL e il portale di Azure. Invece di monitoraggio e ottimizzazione del database manualmente, è possibile delegare alcuni hello di monitoraggio e ottimizzazione tooSQL azioni utilizzando le funzionalità di ottimizzazione automatica del Database. Database SQL automaticamente applica indicazioni, test e verifica ognuno delle prestazioni di hello tooensure azioni ottimizzazione mantiene miglioramento. In questo modo, il Database SQL si adatta automaticamente tooyour del carico di lavoro in modo sicuro e controllato. L'ottimizzazione automatica significa che hello delle prestazioni del database viene accuratamente monitorata e prima e dopo ogni azione di ottimizzazione e se non migliorano le prestazioni di hello, hello ottimizzazione azione viene ripristinato.

Oggi, molti dei nostri partner in esecuzione [App multi-tenant SaaS](sql-database-design-patterns-multi-tenancy-saas-applications.md) sul Database SQL si basa sul toomake che le applicazioni abbiano sempre stabili e prevedibili prestazioni l'ottimizzazione automatica. Questa funzionalità riduce notevole il rischio di hello di disporre di un problema di prestazioni al centro hello della notte hello. Inoltre, in quanto parte del loro clientela Usa anche SQL Server, utilizzano hello indicizzazione uguali a quelli forniti da toohelp Database SQL propri clienti di SQL Server.

Nel database SQL sono disponibili due contesti di ottimizzazione automatica:

- **[Gestione automatica degli indici](sql-database-automatic-tuning.md#automatic-index-management)**: consente di identificare gli indici da aggiungere al database e quelli che è consigliabile rimuovere.
- **[Correzione automatica dei piani](sql-database-automatic-tuning.md#automatic-plan-choice-correction)**: consente di identificare i piani problematici e correggere i problemi di prestazioni dei piani SQL (presto disponibile, già presente in SQL Server 2017).

### <a name="adaptive-query-processing"></a>Elaborazione di query adattiva

Anche se si aggiungono hello [l'elaborazione delle query adattivo](/sql/relational-databases/performance/adaptive-query-processing) famiglia di funzioni tooSQL Database, inclusa l'esecuzione interleaved di funzioni a istruzioni multiple con valori di tabella, commenti e suggerimenti concessione di memoria in modalità batch, batch e join adattivo modalità . Ognuna di queste funzionalità di elaborazione delle query adattivo applica tecniche "informazioni e adattare" simili, contribuendo ulteriori problemi di prestazioni problemi correlati toohistorically query difficili ottimizzazione indirizzo.

### <a name="intelligent-threat-detection"></a>Rilevamento delle minacce intelligente

 [Rilevamento minacce SQL](sql-database-threat-detection.md) sfrutta [controllo del Database SQL](sql-database-auditing.md) toocontinuously monitoraggio SQL Azure database per i dati sensibili tooaccess tentativi potenzialmente dannosi. Rilevamento minacce SQL fornisce un nuovo livello di sicurezza, che consente ai clienti toodetect e risposta toopotential minacce che si verificano fornendo gli avvisi di sicurezza sull'attività anomale. Gli utenti ricevono avvisi in caso di attività di database sospette, potenziali vulnerabilità e attacchi SQL injection, nonché in caso di modelli di accesso ai database anomali. Minaccia SQL gli avvisi di rilevamento forniscono i dettagli dell'attività sospette e consiglieranno azione sulla tooinvestigate e ridurre il rischio di hello. Agli utenti di esplorare hello eventi sospetti toodetermine se hello evento risultati da un tentativo di tooaccess, violazioni o sfruttare i dati nel database di hello. Rilevamento minacce rende semplice tooaddress potenziali minacce toohello database di senza necessità di hello toobe un esperto della sicurezza o gestire i sistemi di monitoraggio di sicurezza avanzata.

## <a name="advanced-security-and-compliance"></a>Sicurezza e conformità avanzate

Database SQL fornisce una gamma di [funzionalità incorporate di sicurezza e conformità](sql-database-security-overview.md) toohelp applicazione soddisfare diversi requisiti di sicurezza e conformità. 

### <a name="auditing-for-compliance-and-security"></a>Controllo per conformità e sicurezza

[Controllo del Database SQL](sql-database-auditing.md) tiene traccia degli eventi di database e li scrive i log di controllo tooan nell'account di archiviazione di Azure. Il controllo consente di agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare problemi aziendali o sospette violazioni della sicurezza.

### <a name="data-encryption-at-rest"></a>Crittografia di dati inattivi

Database SQL [crittografia dati trasparente](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) consente la protezione da minacce hello di attività dannose eseguendo la crittografia in tempo reale e la decrittografia di hello database, i backup associati, e i file di log delle transazioni inattivi senza richiedere modifiche toohello applicazione. A partire da maggio 2017, tutti i nuovi database SQL di Azure creati vengono protetti automaticamente con Transparent Data Encryption (TDE). Transparent Data Encryption è SQL tecnologia di crittografia a riposo richiesto da molti tooprotect standard di conformità furto dei supporti di archiviazione. I clienti possono gestire le chiavi di crittografia TDE hello e altri segreti in modo sicuro e conforme con insieme credenziali chiavi Azure.

### <a name="data-encryption-in-motion"></a>Crittografia dei dati in movimento

Database SQL è hello solo database sistema toooffer protezione dei dati sensibili in fase di trasferimento, inattivi e durante l'esecuzione di query di elaborazione con [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine). Always Encrypted è un primo settore che offre dati ineguagliabile sicurezza contro violazioni della sicurezza che comportano il furto di hello di dati critici. Ad esempio, con crittografia sempre attiva, i numeri di carta di credito dei clienti vengono archiviati crittografati nel database di hello sempre, anche durante l'elaborazione delle query, consentendo di decrittografia punto hello d'uso personale autorizzato o applicazioni che richiedono tooprocess che i dati.

### <a name="dynamic-data-masking"></a>Maschera dati dinamica

[La maschera dati dinamica del Database SQL](sql-database-dynamic-data-masking-get-started.md) limita l'esposizione dei dati sensibili nascondendoli agli utenti con privilegi toonon. Maschera dati dinamica aiuta a impedire che i dati di accesso non autorizzato toosensitive abilitando i clienti toodesignate la quantità di hello dati sensibili tooreveal con un impatto minimo sul livello di applicazione hello. È una funzionalità basata su criteri di sicurezza che consente di nascondere i dati sensibili hello nel set di risultati hello di una query su campi di database designati, senza dati hello hello database non viene modificati.

### <a name="row-level-security"></a>Sicurezza a livello di riga

[Sicurezza a livello di riga](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) consente ai clienti toocontrol accesso toorows in una tabella di database in base alle caratteristiche di hello dell'utente hello esegue una query (ad esempio dal contesto di esecuzione o di appartenenza gruppo). Sicurezza a livello di riga (riga) semplifica la progettazione di hello e la codifica della sicurezza nell'applicazione. E consente le restrizioni tooimplement sull'accesso alle righe di dati. Ad esempio assicurandosi che i lavoratori possano accedere solo le righe di dati che sono pertinenti tootheir reparto o limitare i dati rilevanti tootheir società di un cliente dati accesso tooonly hello.

### <a name="azure-active-directory-integration-and-multi-factor-authentication"></a>Integrazione in Azure Active Directory e autenticazione a più fattori

Consente di Database SQL è toocentrally gestire le identità dell'utente del database e altri servizi Microsoft con [integrazione di Azure Active Directory](sql-database-aad-authentication.md). Questa funzionalità semplifica la gestione delle autorizzazioni e ottimizza la sicurezza. Azure Active Directory supporta [multi-factor authentication](sql-database-ssms-mfa-authentication.md) (MFA) tooincrease dati e applicazione della protezione supportando un singolo processo tramite-in.

### <a name="compliance-certification"></a>Certificazione di conformità

Il database SQL è sottoposto a regolari controlli e ha ottenuto la certificazione per vari standard di conformità. Per ulteriori informazioni, vedere hello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/), in cui è possibile trovare l'elenco più recente di hello di [certificazioni di conformità di Database SQL](https://azure.microsoft.com/support/trust-center/services/).

## <a name="easy-to-use-tools"></a>Strumenti facili da usare

Il database SQL consente di creare e gestire le applicazioni in modo più facile e produttivo. Database SQL consente toofocus per le operazioni più: compilazione di App eccezionali. Per la gestione e lo sviluppo nel database SQL è possibile usare strumenti e competenze già disponibili.

- **[portale di Azure Hello](https://portal.azure.com/)**: un'applicazione basata su web per la gestione di tutti i servizi di Azure 
- **[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)**: un'applicazione scaricabile gratuita, client per la gestione di qualsiasi infrastruttura SQL, da SQL Server tooSQL Database
- **[SQL Server Data Tools in Visual Studio](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)**: applicazione client gratuita e scaricabile per lo sviluppo di database relazionali di SQL Server, database SQL di Azure, pacchetti di Integration Services, modelli di dati di Analysis Services e report di Reporting Services.
- **[Codice di Visual Studio](https://code.visualstudio.com/docs)**: un, scaricabile open source gratuito, editor di codice per Windows, macOS e Linux che supporti le estensioni, tra cui hello [estensione mssql](https://aka.ms/mssql-marketplace) per Microsoft SQL Server, l'esecuzione di query Database SQL di Azure e SQL Data Warehouse.

Database SQL supporta la compilazione di applicazioni con Python, Java, Node.js, PHP, Ruby, .NET su hello MacOS, Linux e Windows. Database SQL supporta hello stesso [raccolte connessioni](sql-database-libraries.md) come SQL Server.

## <a name="engage-with-hello-sql-server-engineering-team"></a>Coinvolgere il team di progettazione di SQL Server hello

- [DBA Stack Exchange](https://dba.stackexchange.com/questions/tagged/sql-server): per domande relative all'amministrazione dei database
- [Stack Overflow](http://stackoverflow.com/questions/tagged/sql-server): per domande relative allo sviluppo
- [Forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver): per domande tecniche
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback): per segnalare bug e richiedere funzionalità
- [Reddit](https://www.reddit.com/r/SQLServer/): per comunicazioni su SQL Server

## <a name="next-steps"></a>Passaggi successivi

- Vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/sql-database/) per singolo database e i confronti di costo di pool elastico e calcolatori.

- Vedere che le guide introduttive tooget che è stato avviato:

  - [Creare un database SQL nel portale di Azure hello](sql-database-get-started-portal.md)  
  - [Creare un database SQL con hello CLI di Azure](sql-database-get-started-cli.md)
  - [Creare un database SQL usando PowerShell](sql-database-get-started-powershell.md)

- Per un set di esempi dell'interfaccia della riga di comando di Azure e di PowerShell, vedere:
  - [Esempi dell'interfaccia della riga di comando di Azure per database SQL](sql-database-cli-samples.md)
  - [Esempi di Azure PowerShell per database SQL](sql-database-powershell-samples.md)
