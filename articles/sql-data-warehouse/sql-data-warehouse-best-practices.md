---
title: procedure consigliate aaaBest per Azure SQL Data Warehouse | Documenti Microsoft
description: Indicazioni e procedure consigliate da conoscere per lo sviluppo di soluzioni per Azure SQL Data Warehouse. Queste indicazioni aiuteranno a svolgere al meglio il lavoro.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 7b698cad-b152-4d33-97f5-5155dfa60f79
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 1f42908fc03e1ca52278a6853d1afe9543d648b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-sql-data-warehouse"></a>Procedure consigliate per Azure SQL Data Warehouse
In questo articolo è una raccolta di molte procedure consigliate che consentono di ottenere prestazioni ottimali tooachieve da Azure SQL Data Warehouse.  Alcuni dei concetti di hello in questo articolo sono tooexplain di base e semplice, altri concetti sono più avanzate e abbiamo scratch appena area hello in questo articolo.  Hello in questo articolo mira toogive si alcuni base compatibile con informazioni aggiuntive e tooraise toofocus aree importanti quando si compila il data warehouse.  Ogni sezione illustra il concetto di tooa e quindi puntare il concetto di hello copertura in maggiore dettaglio di articoli toomore dettagliate.

Chi è alle prime armi con Azure SQL Data Warehouse non deve farsi spaventare dall'articolo.  sequenza di Hello degli argomenti hello è principalmente in ordine di hello di importanza.  Se si avvia concentrandosi su hello innanzitutto alcuni concetti, sarà funzionano correttamente.  Man mano che si acquisisce maggiore familiarità e si diventa più esperti nell'uso di SQL Data Warehouse, rivedere l'articolo ed esaminare altri concetti.  Non avrà lunghe per tutti gli elementi toomake senso.

## <a name="reduce-cost-with-pause-and-scale"></a>Ridurre i costi con sospensione e scalabilità
Una funzionalità chiave di SQL Data Warehouse è hello possibilità toopause quando non si utilizza, che viene arrestata la fatturazione hello delle risorse di calcolo.  Un'altra funzionalità chiave è risorse tooscale possibilità di hello.  La sospensione e la scalabilità può essere eseguita tramite hello portale di Azure o tramite i comandi di PowerShell.  Acquisire familiarità con queste funzionalità, ma può ridurre notevolmente il costo di hello del data warehouse quando non è in uso.  Se si desidera comunque il data warehouse accessibile, è consigliabile tooconsider scalabilità verso il basso toohello più piccolo, un DW100 anziché la sospensione.

Vedere anche [Sospendere le risorse di calcolo][Pause compute resources], [Riavviare le risorse di calcolo][Resume compute resources] e [Ridimensionare le risorse di calcolo].

## <a name="drain-transactions-before-pausing-or-scaling"></a>Scaricare le transazioni prima della sospensione o del ridimensionamento
Quando si sospende o ridimensionare il Data Warehouse di SQL, che le query vengono annullate quando si avvia hello in background hello sospendere o ridimensionare richiesta.  Annullamento di una semplice query di selezione è un'operazione rapida e non ha quasi alcun impatto toohello tempo toopause o ridimensionare l'istanza.  Tuttavia, query transazionale, modificare la struttura di dati o hello dei dati di hello, potrebbe non essere in grado di toostop rapidamente.  **Le query transazionali, per definizione, devono essere completate interamente oppure è necessario il rollback delle modifiche.**  Rollback di operazioni di hello completata da una query transazionale consentono di eseguire lungo o anche più a lungo, la modifica originale hello hello query è stato applicato.  Ad esempio, se si annulla una query che l'eliminazione di righe ed è già in esecuzione per un'ora, potrebbero richiedere sistema hello un'ora tooinsert hello indietro di righe che sono stati eliminati.  Se si esegue pausa o scalabilità durante le transazioni sono in fase di trasferimento, la sospensione o la scalabilità può sembrare tootake molto tempo perché la sospensione e la scalabilità è toowait per hello rollback toocomplete prima che questo possa procedere.

Vedere anche [Informazioni sulle transazioni][Understanding transactions] e [Ottimizzazione delle transazioni][Optimizing transactions]

## <a name="maintain-statistics"></a>Gestire le statistiche
A differenza di SQL Server, che rileva e crea o aggiorna automaticamente le statistiche sulle colonne, SQL Data Warehouse richiede la manutenzione manuale delle statistiche.  Anche se si prevede di toochange sono ottimizzati in hello futura, per ora è toomaintain il tooensure statistiche che hello piani SQL Data Warehouse.  i piani di Hello creati da query optimizer hello sono solo fintanto che le statistiche disponibili hello.  **Creare le statistiche campionate ogni colonna viene avviato tooget un modo semplice con le statistiche.**  È ugualmente importante tooupdate statistiche come modifiche significative succedere tooyour dati.  Un approccio conservativo potrebbe essere tooupdate le statistiche di ogni giorno o dopo ogni carico.  Sono sempre presenti compromessi tra prestazioni e hello costo toocreate e aggiornare le statistiche. Se si ritiene che sta richiedendo troppo tempo toomaintain tutte le statistiche, è necessario frequenti toobe tootry più selettivo sulle statistiche dispongano quali colonne o le colonne di aggiornamento.  Ad esempio, è possibile tooupdate le colonne di data, in cui i nuovi valori possono essere aggiunto, ogni giorno. **Si potrà usufruire hello migliori con le statistiche su colonne coinvolte nel join, le colonne utilizzate nelle hello dove clausola e le colonne disponibili in GROUP BY.**

Vedere anche [Gestire le statistiche delle tabelle][Manage table statistics], [CREATE STATISTICS][CREATE STATISTICS] e [UPDATE STATISTICS][UPDATE STATISTICS]

## <a name="group-insert-statements-into-batches"></a>Raggruppare le istruzioni INSERT in batch
Può eseguire correttamente una tabella di piccole dimensioni tooa carico monouso con un'istruzione INSERT o anche un ricaricamento periodico di una ricerca per le proprie esigenze con un'istruzione come `INSERT INTO MyLookup VALUES (1, 'Type 1')`.  Tuttavia, se è necessario tooload migliaia o milioni di righe per tutto il giorno hello, è possibile che gli inserimenti singleton di soddisfare le.  In alternativa, sviluppare i processi in modo che la scrittura di file tooa e un altro processo subentra periodicamente e carica il file.

Vedere anche [INSERT][INSERT]

## <a name="use-polybase-tooload-and-export-data-quickly"></a>Utilizzare rapidamente PolyBase tooload ed esportare dati
SQL Data Warehouse supporta il caricamento e l'esportazione dei dati attraverso diversi strumenti, tra cui Azure Data Factory, PolyBase e BCP.  Per piccole quantità di dati in cui le prestazioni non sono fondamentali, qualsiasi strumento può essere adeguato per soddisfare le esigenze.  Tuttavia, quando il caricamento o l'esportazione di grandi volumi di dati o di prestazioni elevate sono necessaria, PolyBase è la scelta migliore hello.  PolyBase è progettato tooleverage hello MPP (massiva l'elaborazione parallela) architettura di SQL Data Warehouse e pertanto carica ed esportare ordini di grandezza di dati più velocemente rispetto a qualsiasi altro strumento.  Le operazioni di caricamento di PolyBase possono essere eseguite usando CTAS o INSERT INTO.  **Utilizzando un'istruzione CTAS ridurrà al minimo la registrazione delle transazioni e tooload modo più rapido hello i dati.**  Azure Data Factory supporta anche le operazioni di caricamento di PolyBase.  PolyBase supporta una vasta gamma di formati di file, inclusi i file GZIP.  **velocità effettiva toomaximize quando si utilizzano file di testo gzip, i file di interruzione in più di 60 parallelismo toomaximize i file del carico.**  Per una velocità effettiva totale maggiore, prendere in considerazione il caricamento simultaneo dei dati.

Vedere anche [Caricare i dati][Load data], [Guida per l'uso di PolyBase][Guide for using PolyBase], [Strategie e modelli di caricamento di Azure SQL Data Warehouse][Azure SQL Data Warehouse loading patterns and strategies], [Caricare dati con Azure Data Factory][Load Data with Azure Data Factory], [Spostare dati con Azure Data Factory][Move data with Azure Data Factory], [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] e [Create Table As Select (CTAS)][Create table as select (CTAS)]

## <a name="load-then-query-external-tables"></a>Caricare ed eseguire query su tabelle esterne
Polybase, noto anche come le tabelle esterne, può essere dati tooload modo più veloci di hello, non è ottimale per le query. Le tabelle Polybase di SQL Data Warehouse attualmente supportano solo file BLOB di Azure. Questi file non sono supportati da alcuna risorsa di calcolo.  Di conseguenza, SQL Data Warehouse non è possibile affidare questo lavoro e pertanto deve leggere tutto il file hello caricandolo tootempdb dati di hello tooread degli ordini.  Pertanto, se si dispone di più query che eseguirà una query questi dati, è meglio tooload dati una volta e includono query di utilizzare una tabella locale hello.

Vedere anche [Guida per l'uso di PolyBase][Guide for using PolyBase]

## <a name="hash-distribute-large-tables"></a>Utilizzare la distribuzione hash per le tabelle di grandi dimensioni
Per impostazione predefinita, per le tabelle viene usata la distribuzione round robin.  Questo semplifica per gli utenti tooget cominciare a creare le tabelle senza toodecide come le tabelle devono essere distribuite.  Le tabelle round robin possono funzionare bene per alcuni carichi di lavoro, ma spesso la selezione di una colonna di distribuzione offre prestazioni notevolmente migliori.  Hello più comuni ad esempio quando una tabella distribuita da una colonna di misura ottengano una tabella di Round Robin è quando vengono aggiunti due tabelle dei fatti di grandi dimensioni.  Ad esempio, se si dispone di una tabella orders, che viene distribuita da order_id, e una tabella delle transazioni, che viene distribuita anche da order_id, quando si aggiunge la tabella di transazioni tooyour tabella orders in order_id, la query diventa una query pass-through, ovvero si eliminano operazioni di spostamento dei dati.  Un numero inferiore di passaggi consente una maggiore velocità di esecuzione delle query.  Anche un numero inferiore di operazioni di spostamento consente query più veloci.  Questa superficie hello grana solo di spiegazione. Durante il caricamento di una tabella distribuita, assicurarsi che i dati in ingresso non vengono ordinati nella chiave di distribuzione hello come questo rallenterà il caricamento.  Vedere i collegamenti hello riportato di seguito per la maggior parte ulteriori dettagli su come selezionare una colonna di distribuzione può migliorare le prestazioni e come toodefine una tabella nella clausola WITH hello dell'istruzione di creazione di tabelle distribuita.

Vedere anche [Panoramica sulle tabelle][Table overview], [Distribuzione delle tabelle][Table distribution], [Selecting table distribution][Selecting table distribution] (Selezione della distribuzione delle tabelle), [CREATE TABLE][CREATE TABLE] e [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="do-not-over-partition"></a>Non creare un numero eccessivo di partizioni
Anche se il partizionamento dei dati può essere molto efficace per la gestione dei dati tramite il cambio di partizione o l'ottimizzazione delle analisi con l'eliminazione delle partizioni, un numero eccessivo di partizioni può rallentare le query.  Spesso una strategia di partizionamento che prevede una granularità molto elevata, che potrebbe funzionare bene in SQL Server, potrebbe non essere ideale in SQL Data Warehouse.  Con un numero eccessivo di partizioni può anche ridurre l'efficacia degli indici columnstore cluster hello se ogni partizione dispone di meno di 1 milione di righe.  Tenere presente che hello automaticamente SQL Data Warehouse partizionamento dei dati per l'utente nei 60 database, pertanto se si crea una tabella con 100 partizioni, ciò comporta effettivamente 6000 partizioni.  Ogni carico di lavoro è diverso, pertanto Consiglio migliore hello è tooexperiment con partizionamento toosee la soluzione più adatta per il carico di lavoro.  Prendere in considerazione una granularità inferiore rispetto a quella considerata appropriata in SQL Server.  Prendere ad esempio in considerazione l'uso di partizioni settimanali o mensili invece che giornaliere.

Vedere anche [Partizionamento delle tabelle][Table partitioning]

## <a name="minimize-transaction-sizes"></a>Ridurre al minimo le dimensioni delle transazioni
Le istruzioni INSERT, UPDATE e DELETE vengono eseguite in una transazione e quando si verifica un errore è necessario eseguire il rollback.  hello toominimize potenziale per un lungo rollback, di ridurre al minimo le dimensioni delle transazioni quando possibile.  A tale scopo, è possibile suddividere in parti le istruzioni INSERT, UPDATE e DELETE.  Ad esempio, se si dispone di un'istruzione INSERT che si prevede che tootake 1 ora, se possibile, suddividere hello INSERT in 4 parti, che verranno eseguito ogni 15 minuti.  Utilizzare la registrazione minima particolari, ad esempio un'istruzione CTAS, TRUNCATE, DROP TABLE o inserire tooempty tabelle, il rischio di rollback tooreduce.  I ripristini di un altro modo tooeliminate è toouse metadati solo operazioni come la gestione dei dati del cambio di partizione.  Ad esempio, invece di eseguire tutte le righe di un toodelete istruzione DELETE in una tabella in cui è stato hello order_date nell'ottobre del 2001, è possibile partizionare i dati mensili e quindi partizione di disattivazione hello con i dati per una partizione vuota da un'altra tabella (vedere ALTER Esempi di tabella).  Per le tabelle non partizionate considerare utilizzando dati hello un toowrite di un'istruzione CTAS che si desidera tookeep in una tabella anziché DELETE.  Se una istruzione CTAS accetta hello stessa quantità di tempo, è un toorun operazione molto più sicura ed è con registrazione minima delle transazioni può essere annullata rapidamente se necessario.

Vedere anche [Informazioni sulle transazioni][Understanding transactions], [Ottimizzazione delle transazioni][Optimizing transactions], [Partizionamento delle tabelle][Table partitioning], [TRUNCATE TABLE][TRUNCATE TABLE], [ALTER TABLE][ALTER TABLE] e [Create table as select (CTAS)][Create table as select (CTAS)]

## <a name="use-hello-smallest-possible-column-size"></a>Utilizzare hello più piccolo possibile di colonne dimensione
Quando si definisce l'istruzione DDL, con tipo di dati più piccolo hello che supporterà i dati migliorerà le prestazioni delle query.  Questo aspetto è particolarmente importante per le colonne CHAR e VARCHAR.  Se il valore più lungo di hello in una colonna è di 25 caratteri, quindi definire la colonna come VARCHAR(25).  Evitare di definire tutte le colonne tooa predefiniti elevati caratteri.  Definire inoltre le colonne come VARCHAR quando è sufficiente, invece di usare NVARCHAR.

Vedere anche [Panoramica sulle tabelle][Table overview], [Tipi di dati per le tabelle][Table data types] e [CREATE TABLE][CREATE TABLE]

## <a name="use-temporary-heap-tables-for-transient-data"></a>Utilizzare tabelle heap temporanee per i dati temporanei
Quando si temporaneamente di destinazione dei dati in SQL Data Warehouse, è possibile che utilizza una tabella heap effettuerà hello processo complessivo più velocemente.  Se si sta caricando toostage solo di dati prima di eseguire più trasformazioni, il caricamento della tabella di hello tabella tooheap sarà molto più rapido il caricamento di hello dati tooa cluster nella tabella columnstore.  Inoltre, il caricamento di dati tooa tabella temporanea anche caricherà molto più rapidamente il caricamento di un'archiviazione toopermanent tabella.  Tabelle temporanee iniziano con "#" e sono accessibili solo dalla sessione hello cui è stato creato, in modo che funzionino in scenari limitati.   Le tabelle heap sono definite nella clausola WITH hello di CREATE TABLE.  Se si utilizza una tabella temporanea, è troppo toocreate statistiche in tale tabella temporanea.

Vedere anche [Tabelle temporanee][Temporary tables], [CREATE TABLE][CREATE TABLE] e [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="optimize-clustered-columnstore-tables"></a>Ottimizzare le tabelle columnstore cluster
Gli indici columnstore cluster sono uno dei modi più efficienti di hello che è possibile archiviare i dati in Azure SQL Data Warehouse.  Per impostazione predefinita, le tabelle in SQL Data Warehouse vengono create come tabelle columnstore cluster.  tooget hello ottenere prestazioni ottimali per le query sulle tabelle columnstore, con qualità buona segmento sono importante.  Quando le righe vengono scritti tabelle toocolumnstore eccessivo della memoria e qualità di segmento di columnstore potrebbe risentirne.  La qualità del segmento può essere misurata in base al numero di righe in un gruppo di righe compresso.  Vedere hello [cause di columnstore di scarsa qualità di indice] [ Causes of poor columnstore index quality] in hello [gli indici di tabella] [ Table indexes] articolo per istruzioni dettagliate su il rilevamento e migliorare la qualità di segmento per le tabelle columnstore cluster.  Poiché i segmenti di columnstore di qualità elevata è importante, è un ID di utenti toouse buona norma che si trovano in una classe di risorse di medie o grandi dimensioni hello per il caricamento dei dati.  Hello Dwu meno usate, hello maggiore hello classe di risorse è tooyour tooassign durante il caricamento di utente.

Poiché le tabelle columnstore in genere non push dei dati in un segmento di columnstore compressa fino a quando non sono presenti più di 1 milione di righe per ogni tabella e ogni tabella di SQL Data Warehouse è suddiviso in 60 le tabelle, come regola generale, le tabelle columnstore non trarre vantaggio di una query a meno che la tabella hello abbia più di 60 milioni di righe.  Per la tabella con meno di 60 milioni di righe, potrebbe non essere qualsiasi toohave utile un indice columnstore.  ma potrebbe anche non avere effetti negativi.  Inoltre, se si partizionare i dati, quindi è opportuno tooconsider che ogni partizione sarà necessario toohave 1 milione di righe toobenefit da un indice columnstore cluster.  Se una tabella dispone di 100 partizioni, quindi è necessario almeno 6 miliardi toohave toobenefit di righe da un archivio colonne cluster (60 distribuzioni * 100 partizioni * 1 milione di righe).  Se la tabella non dispone di 6 miliardi di righe in questo esempio, ridurre il numero di hello di partizioni o si consideri l'utilizzo di una tabella heap.  Potrebbe anche essere opportuno toosee prove se è possono ottenere prestazioni migliori con una tabella heap con gli indici secondari, anziché una tabella columnstore.  Le tabelle columnstore al momento non supportano gli indici secondari.

Quando una query su una tabella columnstore, le query verranno eseguite più velocemente se si selezionano solo le colonne hello che è necessario.  

Vedere anche [Indicizzazione delle tabelle][Table indexes], [Guida agli indici columnstore][Columnstore indexes guide] e [Ricompilazione degli indici columnstore][Rebuilding columnstore indexes]

## <a name="use-larger-resource-class-tooimprove-query-performance"></a>Utilizzare più grande risorsa classe tooimprove le prestazioni delle query
SQL Data Warehouse utilizza gruppi di risorse come un tooqueries di memoria tooallocate modo.  Viene fornita hello, tutti gli utenti vengono assegnati a classe di risorse ridotto toohello che garantisce a 100 MB di memoria per ogni distribuzione.  Poiché esistono sempre le 60 distribuzioni e ogni distribuzione viene assegnato un minimo di 100 MB, totale memoria hello wide sistema allocazione è 6.000 MB o poco meno di 6 GB.  In determinati casi, ad esempio join di grandi dimensioni o le tabelle columnstore tooclustered carichi, sfrutterà maggiori delle allocazioni di memoria.  Alcune query, come le operazioni di sola analisi, non traggono alcun vantaggio.  Sul lato capovolto hello, che utilizzano le classi di risorse maggiore influisce sulla concorrenza, in modo da tootake questo in considerazione prima di migrare tutti la classe di risorse di grandi dimensioni tooa gli utenti.

Vedere anche [Gestione della concorrenza e del carico di lavoro][Concurrency and workload management]

## <a name="use-smaller-resource-class-tooincrease-concurrency"></a>Utilizzare una classe di risorse minore tooIncrease concorrenza
Se si è notato che le query utente sembrano toohave un ritardo prolungato, è possibile che gli utenti sono in esecuzione in classi di risorse maggiore e utilizzano molta causando tooqueue altre query di slot di concorrenza.  toosee se le query degli utenti vengono messe in coda, eseguire `SELECT * FROM sys.dm_pdw_waits` toosee se vengono restituite righe.

Vedere anche [Gestione della concorrenza e del carico di lavoro][Concurrency and workload management] e [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="use-dmvs-toomonitor-and-optimize-your-queries"></a>Utilizzare DMV toomonitor e ottimizzare le query
SQL Data Warehouse ha diverse viste a gestione dinamica che può essere utilizzato toomonitor l'esecuzione di query.  Hello monitoraggio articolo seguente illustra in dettaglio le istruzioni dettagliate su come eseguire una query toolook dettagli hello di un'esecuzione.  query di ricerca tooquickly in queste DMV, opzione etichetta hello con le query può essere utile.

Vedere anche [Monitoraggio del carico di lavoro mediante DMV][Monitor your workload using DMVs], [LABEL][LABEL], [OPTION][OPTION], [sys.dm_exec_sessions][sys.dm_exec_sessions], [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests], [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps], [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], [sys.dm_pdw_dms_workers], [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] e [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="other-resources"></a>Altre risorse:
Vedere anche l'articolo sulla [risoluzione dei problemi][Troubleshooting] per informazioni sui problemi più comuni e le relative soluzioni.

Se non viene trovato ciò che stavano cercando in questo articolo, provare a utilizzare hello "Ricerca per documenti" sul lato sinistro hello di toosearch questa pagina tutte di documenti di Azure SQL Data Warehouse hello.  Hello [Forum MSDN di Azure SQL Data Warehouse] [ Azure SQL Data Warehouse MSDN Forum] stato creare come posizione per si tooask domande utenti tooother e toohello gruppo di prodotto di SQL Data Warehouse.  È un monitoraggio attivo questo tooensure forum che le domande in base a un altro utente o uno degli Stati Uniti.  Se si preferiscono tooask domande su Stack Overflow, è necessario anche un [Azure SQL Data Warehouse Stack Overflow Forum][Azure SQL Data Warehouse Stack Overflow Forum].

Infine, utilizzare hello [Azure SQL Data Warehouse Feedback] [ Azure SQL Data Warehouse Feedback] pagina toomake funzionalità richieste.  Le richieste aggiunte o i voti per altre richieste sono utili per definire le priorità per le funzionalità.

<!--Image references-->

<!--Article references-->
[Create a support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Create table as select (CTAS)]: ./sql-data-warehouse-develop-ctas.md
[Table overview]: ./sql-data-warehouse-tables-overview.md
[Table data types]: ./sql-data-warehouse-tables-data-types.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexes]: ./sql-data-warehouse-tables-index.md
[Causes of poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuilding columnstore indexes]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Manage table statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary tables]: ./sql-data-warehouse-tables-temporary.md
[Guide for using PolyBase]: ./sql-data-warehouse-load-polybase-guide.md
[Load data]: ./sql-data-warehouse-overview-load.md
[Move data with Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[Load data with Azure Data Factory]: ./sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Monitor your workload using DMVs]: ./sql-data-warehouse-manage-monitor.md
[Pause compute resources]: ./sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Resume compute resources]: ./sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[Ridimensionare le risorse di calcolo]: ./sql-data-warehouse-manage-compute-overview.md#scale-compute
[Understanding transactions]: ./sql-data-warehouse-develop-transactions.md
[Optimizing transactions]: ./sql-data-warehouse-develop-best-practices-transactions.md
[Troubleshooting]: ./sql-data-warehouse-troubleshoot.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->
[ALTER TABLE]: https://msdn.microsoft.com/library/ms190273.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[CREATE TABLE AS SELECT]: https://msdn.microsoft.com/library/mt204041.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: https://msdn.microsoft.com/library/mt204017.aspx
[INSERT]: https://msdn.microsoft.com/library/ms174335.aspx
[OPTION]: https://msdn.microsoft.com/library/ms190322.aspx
[TRUNCATE TABLE]: https://msdn.microsoft.com/library/ms177570.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx
[sys.dm_exec_sessions]: https://msdn.microsoft.com/library/ms176013.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_request_steps]: https://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: https://msdn.microsoft.com/library/mt203889.aspx
[sys.dm_pdw_dms_workers]: https://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_waits]: https://msdn.microsoft.com/library/mt203893.aspx
[Columnstore indexes guide]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
[Selecting table distribution]: https://blogs.msdn.microsoft.com/sqlcat/2015/08/11/choosing-hash-distributed-table-vs-round-robin-distributed-table-in-azure-sql-dw-service/
[Azure SQL Data Warehouse Feedback]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Azure SQL Data Warehouse MSDN Forum]: https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=AzureSQLDataWarehouse
[Azure SQL Data Warehouse Stack Overflow Forum]:  http://stackoverflow.com/questions/tagged/azure-sqldw
[Azure SQL Data Warehouse loading patterns and strategies]: https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies
