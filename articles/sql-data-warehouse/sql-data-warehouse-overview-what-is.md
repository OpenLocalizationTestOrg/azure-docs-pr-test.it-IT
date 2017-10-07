---
title: "aaaWhat è Azure SQL Data Warehouse? | Microsoft Docs"
description: "Database distribuito di livello aziendale, in grado di elaborare volumi di dati relazionali e non relazionali anche nell'ordine di petabyte. È primo data warehouse cloud del settore hello con aumento, compatta e sospensione in secondi."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: bjhubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 2/28/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 5fefe40879230f123c2e4a90b9c20a35779cf711
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a>Che cos'è SQL Data Warehouse di Azure?
Azure SQL Data Warehouse è un database relazionale MPP (Massively Parallel Processing) basato sul cloud, con possibilità di aumentare il numero di istanze, in grado di elaborare volumi massivi di dati. 

SQL Data Warehouse:

* Combina i database relazionale di SQL Server hello con funzionalità di scalabilità orizzontale di cloud di Azure. 
* Separa l'archiviazione dal calcolo.
* Consente l'aumento, la riduzione, la sospensione o la ripresa del calcolo. 
* Integra tra hello piattaforma Azure.
* Usa Transact-SQL (T-SQL) e gli strumenti di SQL Server.
* È conforme a vari requisiti di sicurezza legali e aziendali, ad esempio SOC e ISO.

Questo articolo descrive le funzionalità principali di hello di SQL Data Warehouse.

## <a name="massively-parallel-processing-architecture"></a>Architettura di elaborazione parallela massiva (MPP)
SQL Data Warehouse è un sistema di database distribuito a elaborazione parallela massiva. Dietro le quinte hello SQL Data Warehouse distribuisce i dati in molti archiviazione di condivisione e unità di elaborazione. Hello dati vengono archiviati in un livello di archiviazione con ridondanza locale Premium su cui collegata in modo dinamico i nodi di calcolo eseguono query. Accetta SQL Data Warehouse che toorunning un approccio "suddividere la parte che" Carica e query complesse. Le richieste vengono ricevute da un nodo di controllo, ottimizzato per la distribuzione e quindi passato tooCompute nodi toodo il proprio lavoro in parallelo.

Grazie alla separazione tra archiviazione e calcolo, SQL Data Warehouse consente di:

* Aumentare o ridurre le dimensioni dello spazio di archiviazione indipendentemente dal calcolo.
* Aumentare o ridurre la potenza senza spostare i dati.
* Sospendere la capacità di calcolo mantenendo intatti i dati e pagando solo per l'archiviazione.
* Riprendere le capacità di calcolo durante l'orario operativo.

Hello diagramma seguente mostra architettura hello in modo più dettagliato.

![Architettura di SQL Data Warehouse][1]

**Nodo di controllo:** nodo di controllo del codice hello gestisce e consente di ottimizzare le query. È front-end hello che interagisce con tutte le applicazioni e le connessioni. In SQL Data Warehouse, il nodo di controllo del codice hello è supportato dal Database SQL e connessione tooit esegue la ricerca e rappresenti hello stesso. In area hello, il nodo di controllo del codice hello coordina tutti i calcoli richiesti e lo spostamento dei dati di hello toorun query parallele sui dati distribuiti. Quando si invia un tooSQL query T-SQL Data Warehouse, il nodo di controllo del codice hello li trasforma in query distinte eseguite su ogni nodo di calcolo in parallelo.

**Nodi di calcolo:** fungono da nodi di calcolo hello power hello dietro SQL Data Warehouse. Sono database SQL che archiviano i dati ed elaborano le query. Quando si aggiungono dati, SQL Data Warehouse consente di distribuire i nodi di calcolo tooyour hello righe. nodi di calcolo Hello sono lavoratori hello che eseguono query parallele hello sui dati. Dopo l'elaborazione, passano nodo di controllo del codice hello risultati toohello indietro. query di hello toofinish, il nodo di controllo del codice hello aggrega i risultati di hello e restituisce hello risultato finale.

**Archiviazione** : i dati vengono memorizzati nell'archivio BLOB di Azure. Quando i nodi di calcolo di interagire con i dati, è scrivere e leggere tooand direttamente dall'archiviazione blob. Poiché l'archiviazione di Azure si espande in modo trasparente e notevolmente, è possibile eseguire SQL Data Warehouse hello stesso. Poiché elaborazione e archiviazione sono indipendenti, SQL Data Warehouse può ridimensionare automaticamente le risorse di archiviazione separatamente dal ridimensionamento delle risorse di calcolo e viceversa. Archiviazione Blob di Azure è completamente a tolleranza di errore e semplifica hello backup e ripristino.

**Data Movement Service:** servizio lo spostamento dei dati (DMS) consente di spostare dati tra i nodi di hello. DMS offre hello calcolo nodi accesso toodata necessarie di join e aggregazioni. DMS non è un servizio di Azure. È un servizio Windows che viene eseguito insieme ai Database SQL in tutti i nodi di hello. DMS è un processo in background con il quale non è possibile interagire direttamente. Tuttavia, è possibile visualizzare piani di query toosee quando si verificano operazioni DMS, poiché lo spostamento dei dati è necessario toorun ogni query in parallelo.

## <a name="optimized-for-data-warehouse-workloads"></a>Ottimizzato per carichi di lavoro di data warehouse
approccio MPP Hello è supportato da diverse ottimizzazioni del data warehouse prestazioni specifici, tra cui:

* Un'utilità di ottimizzazione delle query distribuita e un set di statistiche complesse su tutti i dati. Utilizza le informazioni sulla distribuzione e la dimensione dei dati, il servizio di hello è toooptimize in grado di query a valutare i costi di hello delle operazioni di query distribuita specifica.
* Le tecniche e algoritmi avanzati integrati in dati hello spostamento processo tooefficiently spostare i dati tra le risorse di elaborazione come query hello tooperform necessarie. Queste operazioni di spostamento dei dati sono incorporate e tutte le ottimizzazioni toohello Data Movement Service è stata eseguita automaticamente.
* Indici **columnstore** cluster per impostazione predefinita. Con l'archiviazione basata su colonne, SQL Data Warehouse Ottiene medio 5 i guadagni di compressione x rispetto all'archiviazione tradizionale orientata alle righe e di too10x o ulteriori miglioramenti delle prestazioni di query. Le query di Analitica che richiedono tooscan un numero elevato di righe funziona meglio con gli indici columnstore.


## <a name="predictable-and-scalable-performance-with-data-warehouse-units"></a>Prestazioni prevedibili e scalabili con Unità Data Warehouse (DWU)
SQL Data Warehouse è realizzato con tecnologie simili a quelle usate per Database SQL e questo significa che gli utenti possono aspettarsi prestazioni coerenti e prevedibili per le query analitiche. Gli utenti dovrebbero toosee scala di prestazioni in modo lineare in cui aggiungere o sottrarre nodi di calcolo. Allocazione di risorse tooyour SQL Data Warehouse viene misurato in unità di Data Warehouse (Dwu). Dwu sono una misura delle risorse sottostanti, ad esempio CPU, memoria, IOPS, vengono allocati tooyour SQL Data Warehouse. Aumentare il numero di hello Dwu aumenta le risorse e le prestazioni. In particolare, si usano le DWU per poter eseguire queste operazioni:

* Si è in grado di tooscale il data warehouse senza doversi preoccupare hello hardware o software.
* È possibile prevedere miglioramento delle prestazioni per un livello DWU prima di modificare il calcolo di hello del data warehouse.
* Hello sottostante hardware e software dell'istanza può modificare o spostare senza influire sulle prestazioni del carico di lavoro.
* Microsoft può migliorare hello sottostante l'architettura del servizio hello senza influire sulle prestazioni di hello del carico di lavoro.
* Microsoft può migliorare rapidamente le prestazioni in SQL Data Warehouse, in modo che sia scalabile e in modo uniforme effetti hello sistema.

Le Unità Data Warehouse offrono una misura di tre metriche strettamente correlate alle prestazioni del carico di lavoro di data warehousing. esempio Hello chiave scala metrica di carico di lavoro in modo lineare con hello Dwu.

**Analisi/aggregazione:** una query di data warehousing standard che esamina un numero elevato di righe e quindi esegue un'aggregazione complessa. Questa è un'operazione con uso intensivo di I/O e CPU.

**Caricamento:** hello dati tooingest possibilità in servizio hello. Si ottengono prestazioni ottimali per i carichi con PolyBase da BLOB del servizio di archiviazione di Azure o Azure Data Lake. Questa metrica è progettato toostress rete e gli aspetti della CPU del servizio di hello.

**Creare una tabella come Select (un'istruzione CTAS):** un'istruzione CTAS misura hello possibilità toocopy una tabella. Tale attività implica la lettura dei dati dall'archivio, distribuirlo in nodi di hello del dispositivo hello e la scrittura toostorage nuovamente. È un'operazione con uso intensivo di CPU, I/O e rete.

## <a name="built-on-sql-server"></a>Basato su SQL Server
SQL Data Warehouse è basato sul motore di database relazionale di SQL Server hello e include molte funzionalità hello desiderato da un enterprise data warehouse. Se si conosce già T-SQL, è facile tootransfer il tooSQL Knowledge Base Data Warehouse. Se sono avanzate o solo informazioni introduttive, esempi di hello in documentazione hello consente di iniziare. In generale, si pensi a modo hello che gli elementi di linguaggio hello di SQL Data Warehouse è stata creata come indicato di seguito:

* SQL Data Warehouse usa la sintassi T-SQL per molte operazioni. Supporta anche un'ampia gamma di costrutti SQL tradizionali, ad esempio stored procedure, funzioni definite dall'utente, partizionamento delle tabelle, indici e regole di confronto.
* SQL Data Warehouse include anche varie funzionalità recenti di SQL Server, tra cui gli indici **columnstore** cluster, l'integrazione di PolyBase e il controllo dei dati, inclusa la valutazione delle minacce.
* Alcuni elementi del linguaggio T-SQL che sono meno comune per i carichi di lavoro di data warehouse o più recente tooSQL Server, potrebbero non essere attualmente disponibili. Per ulteriori informazioni, vedere hello [documentazione per la migrazione][Migration documentation].

Con hello Transact-SQL e compatibilità di funzionalità tra SQL Server, SQL Data Warehouse, Database SQL e Analitica Platform System, è possibile sviluppare una soluzione adatta alle proprie esigenze di dati. È possibile decidere dove tookeep i dati, basati sulle prestazioni, sicurezza e i requisiti di scala e quindi trasferire i dati in base alle esigenze tra sistemi diversi.

## <a name="data-protection"></a>Protezione dati
SQL Data Warehouse archivia tutti i dati nella risorsa di archiviazione con ridondanza locale Premium di Azure. Più copie di sincrone dei dati di hello vengono mantenute nella protezione hello dati locale center tooguarantee trasparente dei dati in caso di errori localizzata. SQL Data Warehouse esegue anche il backup automatico dei database attivi (non in pausa) a intervalli regolari usando gli snapshot di Archiviazione di Azure. toolearn ulteriori informazioni su backup e ripristino di funzionamento, vedere hello [Panoramica di Backup e ripristino][Backup and restore overview].

## <a name="integrated-with-microsoft-tools"></a>Integrato con strumenti di Microsoft
SQL Data Warehouse si integra anche molti strumenti hello gli utenti potrebbero avere familiari con SQL Server. Questi strumenti comprendono:

**Strumenti tradizionali di SQL Server:** SQL Data Warehouse è completamente integrato con SQL Server Analysis Services, Integration Services e Reporting Services.

**Strumenti basati sul cloud:** SQL Data Warehouse può essere integrato con vari servizi in Azure, tra cui Data factory, Analisi di flusso, Machine Learning e Power BI. Per un elenco più completo, vedere la [panoramica degli strumenti integrati][Integrated tools overview].

**Strumenti di terze parti:** molti provider di strumenti di terze parti hanno certificato l'integrazione dei propri strumenti con SQL Data Warehouse. Per l'elenco completo, vedere [Partner di soluzioni per SQL Data Warehouse][SQL Data Warehouse solution partners].

## <a name="hybrid-data-sources-scenarios"></a>Scenari di origini dati ibride
Polybase consente tooleverage i dati da origini diverse tramite comandi comuni di T-SQL. Polybase consente tooquery dati non relazionali contenuti in archiviazione Blob di Azure come se fosse una normale tabella. Utilizzare i dati di Polybase tooquery non relazionali o dati non relazionali tooimport in SQL Data Warehouse.

* PolyBase utilizza i dati non relazionali tooaccess di tabelle esterne. le definizioni di tabella Hello vengono archiviate in SQL Data Warehouse, è possibile accedervi tramite SQL e strumenti quali si accede a dati relazionali normale.
* Polybase è agnostico nella relativa integrazione, Espone hello stesse caratteristiche e funzionalità tooall hello le origini che supporta. dati Hello letti da Polybase possono essere in vari formati, tra cui file delimitato da virgole o ORC.
* PolyBase può essere l'archiviazione di blob tooaccess utilizzato viene utilizzato anche come spazio di archiviazione per un cluster HDInsight. Questo consente di accedere toohello stessi dati non relazionali e strumenti.

## <a name="sla"></a>Contratto di servizio
SQL Data Warehouse offre un contratto di servizio a livello di prodotto come parte del Contratto di servizio di Microsoft Online Services. Per altre informazioni, vedere [Contratto di servizio per SQL Data Warehouse][SLA for SQL Data Warehouse]. Per informazioni di contratto di servizio su tutti gli altri prodotti è possibile visitare hello [i contratti di servizio] Azure pagina o scaricarli in hello [multilicenza] [ Volume Licensing] pagina. 

## <a name="next-steps"></a>Passaggi successivi
Dopo avere esaminato su SQL Data Warehouse, consultare come tooquickly [creare un Data Warehouse SQL] [ create a SQL Data Warehouse] e [caricare dati di esempio][load sample data]. Se si tooAzure nuova, è possibile hello [glossario di Azure] [ Azure glossary] utile quando si verificano nuovi termini. Oppure vedere alcune delle altre risorse disponibili per SQL Data Warehouse.  

* [Casi di successo dei clienti]
* [Blog]
* [Richieste di funzionalità]
* [Video]
* [Blog Customer Advisory Team]
* [Creare un ticket di supporto]
* [Forum MSDN]
* [Forum su Stack Overflow]
* [Twitter]

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[Creare un ticket di supporto]: ./sql-data-warehouse-get-started-create-support-ticket.md
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
[Casi di successo dei clienti]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse
[Blog]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blog Customer Advisory Team]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Richieste di funzionalità]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Forum MSDN]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse
[Forum su Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Video]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/en-us/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
[i contratti di servizio]: https://azure.microsoft.com/en-us/support/legal/sla/
