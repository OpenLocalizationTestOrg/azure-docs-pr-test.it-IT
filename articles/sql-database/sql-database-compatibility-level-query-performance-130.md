---
title: "il livello di compatibilità aaaDatabase 130 - Database SQL di Azure | Documenti Microsoft"
description: "In questo articolo, è esplorare hello vantaggi offerti dall'esecuzione di Database SQL di Azure a livello di compatibilità 130 e sfruttando i vantaggi di hello nuovo query Optimizer è hello e funzionalità del processore di query. Vengono inoltre affrontati hello possibili effetti collaterali sulle prestazioni delle query hello per le applicazioni SQL hello esistenti."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a>Miglioramento delle prestazioni delle query con il livello di compatibilità 130 nel database SQL di Azure
Database SQL di Azure è in esecuzione in modo trasparente centinaia di migliaia di database con molti livelli di compatibilità diversi, mantenendo e garantendo hello compatibilità toohello corrispondente versione di Microsoft SQL Server per tutti i clienti!

In questo articolo, è esplorare vantaggi hello in esecuzione il database SQL di Azure a livello di compatibilità 130 e sfruttare i vantaggi di hello nuovo query Optimizer è hello e funzionalità del processore di query. Vengono inoltre affrontati hello possibili effetti collaterali sulle prestazioni delle query hello per le applicazioni SQL hello esistenti.

Come promemoria della cronologia, l'allineamento di hello di livelli di compatibilità toodefault versioni SQL sono i seguenti:

* 100: in SQL Server 2008 e database SQL di Azure versione 11.
* 110: in SQL Server 2012 e database SQL di Azure versione 11.
* 120: in SQL Server 2014 e database SQL di Azure versione 12.
* 130: in SQL Server 2016 e database SQL di Azure versione 12.

> [!IMPORTANT]
> A partire da **mid-giugno 2016**, nel Database di SQL Azure, il livello di compatibilità predefinito hello sarà 130 anziché 120 per **appena creato** database.
> 
> I database creati prima della metà di giugno 2016 *non* saranno interessati dalla modifica e manterranno il livello di compatibilità corrente (100, 110 o 120). I database migrati da Database SQL di Azure versione V11 tooV12 avranno un livello di compatibilità pari a 100 o 110. 
> 

## <a name="about-compatibility-level-130"></a>Informazioni sul livello di compatibilità 130
Se si desidera tooknow hello livello di compatibilità corrente del database, eseguire innanzitutto hello seguente istruzione Transact-SQL.

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


Prima di questa modifica toolevel 130 accade per **appena** create database, si esaminare questa modifica novità su alcuni esempi di query molto semplice e vedere come tutti gli utenti possono trarre vantaggio da esso.

L'elaborazione delle query nei database relazionali possono essere molto complessi e può causare toolots computer scienza e matematiche toounderstand hello inerente scelte di progettazione e i comportamenti. In questo documento, contenuto hello è stato intenzionalmente semplificate tooensure che chiunque concetti tecnici minima può comprendere hello impatto della modifica del livello di compatibilità hello e determinare come è possibile trarre vantaggio di applicazioni.

Di seguito hanno una sintesi quale livello di compatibilità 130 hello visualizzata nella tabella hello.  Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx):

* può essere multithreading Hello operazione di inserimento di un'istruzione Insert select o può avere un piano parallelo, mentre prima dell'operazione a thread singolo.
* Le tabelle con ottimizzazione per la memoria e le query sulle variabili di tabella ora possono avere piani paralleli. In precedenza l'operazione era a thread singolo.
* Le statistiche per la tabella con ottimizzazione per la memoria ora possono essere campionate e vengono aggiornate automaticamente. Per altre informazioni, vedere [Novità (Motore di database): OLTP in memoria](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) .
* Modifiche alla modalità batch rispetto alla modalità riga con gli indici columnstore:
  * L'ordinamento in una tabella con un indice columnstore viene ora eseguito in modalità batch.
  * Le aggregazioni finestra ora vengono eseguite in modalità batch, ad esempio con istruzioni TSQL LAG/LEAD.
  * Le query sulle tabelle columnstore con più clausole distinte operano in modalità batch.
  * Anche le query in esecuzione con DOP=1 o con un piano seriale vengono eseguite in modalità batch.
* Miglioramenti di stima della cardinalità provengano effettivamente con livello di compatibilità 120, ma se si esegue in un livello di compatibilità inferiore (ad esempio 100 o 110), hello spostamento toocompatibility livello 130 anche porterà questi miglioramenti e questi possono anche per ultimo, sfruttare le prestazioni di query hello delle applicazioni.

## <a name="practicing-compatibility-level-130"></a>Esercitazione sul livello di compatibilità 130
Primo entriamo alcune tabelle, indici e dati casuali creati toopractice alcune di queste nuove funzionalità. esempi di script TSQL Hello possono essere eseguiti in SQL Server 2016 o in Database SQL di Azure. Tuttavia, quando si crea un database SQL di Azure, assicurarsi scegliere un minimo di hello P2 database perché è necessario almeno un paio di core tooallow multithreading e quindi sfruttare queste funzionalità.

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


A questo punto, si dispone di un toosome aspetto delle funzionalità di elaborazione delle Query hello in arrivo con livello di compatibilità 130.

## <a name="parallel-insert"></a>INSERT in parallelo
L'esecuzione di istruzioni TSQL hello seguente esegue hello dell'operazione di inserimento nel livello di compatibilità 120 e 130, che consente di eseguire rispettivamente hello operazione di inserimento in un modello a thread singolo (120) e in un modello a thread multipli (130).

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


Richiedendo piano di query effettivo hello hello, esaminando la rappresentazione grafica o il relativo contenuto XML, è possibile determinare quale funzione è organo la stima della cardinalità. Esaminando i piani hello side-by-side in figura 1, si vede chiaramente che hello colonna Store inserire esecuzione passa dalla seriale in 120 tooparallel 130. Inoltre, poiché tale modifica hello dell'icona di hello iteratore nel piano di 130 hello con due frecce parallele, viene effettivamente parallela relativa fatto hello che ora hello esecuzione iteratore. Se si dispone di grandi dimensioni toocomplete di operazioni di inserimento, l'esecuzione parallela hello, collegato toohello numero di core, che hai a disposizione per il database di hello, offre prestazioni migliori; backup tooa 100 volte più veloce in base alla situazione specifica.

*Figura 1: Inserire modifiche apportate all'operazione seriale tooparallel con livello di compatibilità 130.*

![Figura 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a>Modalità batch seriale
Analogamente, lo spostamento di livello toocompatibility 130 durante l'elaborazione delle righe di dati consente l'elaborazione in modalità batch. In primo luogo, le operazioni in modalità batch sono disponibili solo in presenza di un indice columnstore. In secondo luogo, un batch in genere rappresenta ~ 900 righe e utilizza una logica di codice ottimizzata per la CPU multicore, velocità effettiva più elevata di memoria e direttamente sfrutta hello dati compressi di hello archivio colonne se possibile. In queste condizioni, SQL Server 2016 può elaborare ~ 900 righe in una sola volta, anziché la 1 riga in fase di hello e di conseguenza, hello costo complessivo generale dell'operazione hello ora condiviso da hello dell'intero batch, riducendo costi riga hello complessiva. La quantità di operazioni combinate con compressione dell'archivio colonne hello fondamentalmente condivisa riduce la latenza di hello coinvolto in un'operazione in modalità batch selezionare. È possibile trovare ulteriori informazioni sull'archivio colonna hello e modalità al batch [Guida agli indici Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Come viene visualizzata di sotto, osservando hello query piani side-by-side nella figura 2, possiamo vedere che la modalità di elaborazione hello è stato modificato con il livello di compatibilità di hello e di conseguenza, quando si eseguono query hello in sia a livello di compatibilità del tutto, possiamo vedere che la maggior parte del tempo di elaborazione hello viene impiegato per riga (% 86) confrontati toohello batch una modalità (% 14), in cui sono stati elaborati 2 batch. Aumentare i set di dati hello, hello vantaggio aumenterà.

*Figura 2: Selezionare le modifiche di operazione dalla modalità seriale toobatch con livello di compatibilità 130.*

![Figura 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a>Modalità batch per l'esecuzione dell'ordinamento
Transizione di hello simile toohello precedente, ma l'operazione di ordinamento applicati tooa, dalla riga (livello di compatibilità 120) toobatch modalità (livello di compatibilità 130) consente di migliorare le prestazioni hello dell'operazione di ordinamento per hello hello gli stessi motivi.

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Visibile side-by-side nella figura 3, possiamo vedere che l'operazione di ordinamento hello in modalità riga rappresenta 81% di hello costo, mentre la modalità batch hello rappresenta solo % 19 del costo di hello (rispettivamente 81% e % 56 Ordina hello stesso).

*Figura 3: Operazione di ordinamento viene modificata dalla modalità a riga toobatch con livello di compatibilità 130.*

![Figura 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

Ovviamente, questi esempi solo contengono decine di migliaia di righe, ovvero nulla quando si esaminano i dati di hello disponibili nella maggior parte dei server SQL questi giorni. Solo questi su milioni di righe invece progetto, e questo può essere convertita in corso di esecuzione per ogni giorno in sospeso di natura hello del carico di lavoro di altri.

## <a name="cardinality-estimation-ce-improvements"></a>Miglioramenti apportati alla stima di cardinalità (CE)
Introdotti con SQL Server 2014, qualsiasi database in esecuzione in un livello di compatibilità 120 sopra renderà hello nuove funzionalità di stima della cardinalità. In pratica, la stima della cardinalità è logica hello utilizzato toodetermine come SQL server eseguirà una query in base al suo costo stimato. stima Hello viene calcolata utilizzando input da statistiche associate agli oggetti coinvolti nella query. In pratica, a livello generale, le funzioni di stima della cardinalità riga conteggio stime insieme alle informazioni sulla distribuzione dei valori hello, Conteggio valori distinct, hello e conteggi duplicati contenuti in hello tabelle e gli oggetti a cui fa riferimento nella query hello. Commette queste stime, può causare i/o disco toounnecessary scadenza tooinsufficient concessioni di memoria (ad esempio TempDB spill) o tooa selezione di un'esecuzione del piano seriale in una parallela alcuni esecuzione, tooname del piano. Conclusione, le stime non corrette possono causare tooan un calo delle prestazioni complessive hello di esecuzione di query. In hello altri lato, stime migliori, eseguire stime più accurate, le esecuzioni di query toobetter lead!

Come accennato in precedenza, le ottimizzazioni query e le stime sono pochi complessi, ma se si desidera toolearn informazioni sui piani di query e stima della cardinalità, è possibile fare riferimento documento toohello [l'ottimizzazione di piani di Query con hello SQL Server 2014 Strumento di stima della cardinalità](https://msdn.microsoft.com/library/dn673537.aspx) per un approfondimento.

## <a name="which-cardinality-estimation-do-you-currently-use"></a>Stima di cardinalità corrente
toodetermine in cui la stima della cardinalità delle query sono in esecuzione, si solo query di utilizzare hello esempi di seguito. Si noti che questo primo esempio verrà eseguiti a livello di compatibilità 110, pertanto l'utilizzo di hello delle funzioni di stima della cardinalità precedente hello.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Al termine dell'esecuzione, fare clic sul collegamento di hello XML ed esaminare le proprietà di hello del primo iteratore hello come illustrato di seguito. Annotare il nome di proprietà hello chiamato CardinalityEstimationModelVersion attualmente impostato su 70. Questo non significa che il livello di compatibilità database hello è impostato toohello versione di SQL Server 7.0 (è impostato su 110 come visibile nelle istruzioni TSQL hello precedente), ma il valore di hello 70 rappresenta semplicemente hello legacy stima della cardinalità funzionalità disponibili a partire da SQL Server 7.0, con cui non erano revisioni principali fino a SQL Server 2014 (che viene fornito con un livello di compatibilità pari a 120).

*Figura 4: hello CardinalityEstimationModelVersion è impostato too70 quando si utilizza un livello di compatibilità 110 o inferiore.*

![Figura 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

In alternativa, è possibile modificare too130 livello di compatibilità hello e disabilitare l'uso di hello della nuova funzione di stima della cardinalità hello utilizzando hello LEGACY_CARDINALITY_ESTIMATION impostare tooON con [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx). Questo verrà essere esattamente hello come utilizzando 110 da un punto di vista della funzione di stima della cardinalità, utilizzando il livello di compatibilità di elaborazione delle query più recente hello. In questo modo, è possibile trarre vantaggio dalla nuova query hello l'elaborazione delle funzionalità con livello di compatibilità più recente di hello (vale a dire la modalità batch), ma comunque si basano sulla funzionalità di stima della cardinalità precedente hello, se necessario.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Il semplice spostamento toohello livello di compatibilità 120 o 130 abilita la funzionalità di hello nuova stima della cardinalità. In tal caso, predefinito hello CardinalityEstimationModelVersion verrà impostato di conseguenza too120 o 130 come viene visualizzata di seguito.

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


*Figura 5: hello CardinalityEstimationModelVersion è impostato too130 quando si utilizza un livello di compatibilità di 130.*

![Figura 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a>Differenze di stima della cardinalità hello che
A questo punto, eseguire leggermente più complesso di query che includono un INNER JOIN con una clausola WHERE con alcuni predicati e diamo un'occhiata hello stima del conteggio delle righe da una funzione di stima della cardinalità precedente hello prima.

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


In modo efficace per eseguire questa query restituisce 200,704 righe, mentre hello riga stima con funzionalità di stima della cardinalità precedente hello attestazioni 194,284 righe. Ovviamente, come accennato prima, questi risultati conteggio righe variano la frequenza con cui è stato eseguito hello degli esempi precedenti, che consente di popolare le tabelle di esempio hello in ogni esecuzione. Ovviamente, predicati di hello nella query avrà inoltre influire sulla stima effettivo di hello oltre a forma di tabella hello, il contenuto dei dati e come questi dati sono effettivamente correlati tra loro.

*Figura 6: stima del conteggio delle righe hello è 194,284 o 6.000 righe disattivata dalle righe di hello 200,704 previsto.*

![Figura 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

In hello allo stesso modo, verrà ora eseguire hello stessa query con nuove funzionalità di stima della cardinalità hello.

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Analizzando hello riportato di seguito, è ora visualizzare che tale stima riga hello è 202,877, o molto inferiore e superiore a quello hello la stima della cardinalità precedente.

*Figura 7: stima del conteggio delle righe hello è 202,877, anziché 194,284.*

![Figura 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

In realtà, il set di risultati di hello è 200,704 righe (tutti i relativi a seconda dei casi la frequenza con cui è stato eseguito nelle query hello hello degli esempi precedenti, ma ancora più importante, poiché hello TSQL utilizza l'istruzione di hello rand (), i valori effettivi hello restituiti possono variare da toohello esecuzione uno accanto). Pertanto, in questo particolare esempio hello nuova stima della cardinalità consente valutare il numero di hello di righe perché 202,877 è molto più simile too200, 704, rispetto a 194,284! Infine, se si modifica una clausola WHERE predicati tooequality hello (invece di ">" per l'istanza), questo esegua stime hello tra hello vecchia e nuova funzione di cardinalità più diversi, a seconda di come numero massimo di corrispondenze è possibile ottenere.

In questo caso, naturalmente, una differenza di circa 6000 righe rispetto al conteggio effettivo non rappresenta una grande quantità di dati, in alcune situazioni. A questo punto, trasporre questo toomillions di righe tra più tabelle e query più complesse e a volte hello stima possa essere spostate di milioni di righe e pertanto hello rischio di prelievo-up hello errato piano di esecuzione, o la richiesta di memoria insufficiente concede iniziali tooTempDB spill e pertanto più i/o, sono molto più elevate.

Se si hanno l'opportunità di hello, esercitarsi a confronto con le query più comuni e di un set di dati e visualizzare autonomamente di quanto alcune delle stime di hello nuovi e precedenti sono interessate, mentre alcuni potrebbe diventare semplicemente più esterno dalla realtà hello o alcuni altri solo semplicemente più vicino toohello effettivo delle righe conta effettivamente restituiti in set di risultati hello. Tutti i relativi a seconda della forma hello di query, le caratteristiche del database SQL di Azure hello, natura hello e dimensioni hello del set di dati e le statistiche di hello disponibili su di essi. Se è stata creata l'istanza di Database SQL di Azure, la query hello optimizer disporrà toobuild viene eseguita la conoscenza da zero anziché riutilizzo delle statistiche di query precedente hello. In tal caso, le stime hello sono molto contestuali e quasi specifico tooevery situazione di server e dell'applicazione. È un aspetto importante di tookeep presente.

## <a name="some-considerations-tootake-into-account"></a>Tootake alcune considerazioni in considerazione
Sebbene la maggior parte dei carichi di lavoro può costituire un vantaggio a livello di compatibilità di hello 130, prima di adottare il livello di compatibilità hello per l'ambiente di produzione, fondamentalmente sono disponibili 3 opzioni:

1. Si sposta il livello di toocompatibility 130 e vedere modalità di esecuzione delle operazioni. Nel caso in cui si nota che alcuni regressioni, è appena sufficiente impostare tooits indietro di hello compatibilità livello livello originale, o mantenere 130 e annullare solo la modalità legacy di hello stima della cardinalità toohello indietro (come descritto in precedenza, questo singolarmente potrebbe risolvere il problema di hello).
2. Testare le applicazioni esistenti in carico di produzione simile, ottimizzare e convalidare le prestazioni di hello prima di passare tooproduction. In caso di problemi, stesso come sopra, è possibile sempre tornare indietro a livello di compatibilità originale toohello o sufficiente invertire la modalità legacy di hello stima della cardinalità toohello indietro.
3. Come opzione finale e hello funzionalità archivio Query hello tooleverage queste domande, è più recente tooaddress modo. Quest'ultima opzione rappresenta il modo più recente di risolvere il problema ed è anche l'opzione consigliata. analisi di hello tooassist delle query in compatibilità livello 120 o inferiore rispetto a 130, non consiglia sufficiente toouse archivio Query. Archivio query è disponibile con la versione più recente di hello del Database SQL di Azure V12, ed è concepita toohelp è la risoluzione dei problemi di prestazioni di query. Hello archivio Query può essere paragonato a un'utilità di traccia eventi per il database di raccogliere e presentare informazioni cronologiche su tutte le query. Questo semplifica l'analisi forense prestazioni riducendo hello ora toodiagnose notevolmente più semplice e risolve i problemi. Per altre informazioni, vedere il post di blog relativo ad [Archivio query, la scatola nera del database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).

In generale, se già associato un set di database in esecuzione a livello di compatibilità 120 o di sotto e pianificare la toomove hello alcuni di essi too130, o perché il carico di lavoro automaticamente il provisioning di nuovi database che verrà presto impostazione too130 predefinito, provare a segue Hello:

* Prima di modificare toohello nuovo livello di compatibilità nell'ambiente di produzione, abilitare l'archivio Query. È possibile fare riferimento troppo[modificare hello archivio Query hello modalità di compatibilità del Database e utilizzare](https://msdn.microsoft.com/library/bb895281.aspx) per ulteriori informazioni.
* Testare quindi i carichi di lavoro sono di importanza critica con dati rappresentativi e query di un ambiente di produzione e confrontare così le prestazioni hello si è verificato e come indicato dall'archivio Query. Se si verificano alcuni regressioni, è possibile identificare hello query regredite con archivio Query hello e utilizzare l'opzione dall'archivio Query di forzatura del piano hello (noto anche come prevede il blocco). In tal caso, si definitivamente rimanere con livello di compatibilità hello 130 e utilizza il piano di query precedente hello come suggerito dal hello archivio Query.
* Se si desidera tooleverage nuove caratteristiche e funzionalità di Database SQL di Azure (che è in esecuzione SQL Server 2016), ma che sono sensibili toochanges dovuta a livello di compatibilità di hello 130, come ultima risorsa, è possibile forzare il nuovo livello di compatibilità di hello livello toohello che soddisfi il carico di lavoro utilizzando un'istruzione ALTER DATABASE. Ma prima di tutto, tale piano di archivio Query hello aggiunta l'opzione è la migliore opzione perché non si utilizza 130 è fondamentalmente sempre al livello di funzionalità hello di una versione precedente di SQL Server.
* Se si dispone di applicazioni multi-tenant che si estende su più database, potrebbe essere necessario tooupdate hello provisioning logica del tooensure database un livello di compatibilità coerente in tutti i database; quelle precedenti e appena sottoposti a provisioning. Le prestazioni del carico di lavoro dell'applicazione potrebbe essere fatto toohello sensibili che alcuni database sono in esecuzione con livelli di compatibilità diversi e pertanto la coerenza a livello di compatibilità in qualsiasi database potrebbe essere necessarie in ordine tooprovide hello stesso esperienza clienti tooyour tutti tra Lavagna hello. Si noti che non è un Imponi la risposta dipende influenza l'applicazione dal livello di compatibilità hello.
* Infine, hello stima della cardinalità, nonché come modifica livello di compatibilità hello, prima di procedere nell'ambiente di produzione, è consigliabile tootest il carico di lavoro di produzione in hello nuove condizioni toodetermine se l'applicazione trae vantaggio da miglioramenti di stima della cardinalità Hello.

## <a name="conclusion"></a>Conclusioni
L'utilizzo di Database SQL di Azure toobenefit da tutti i miglioramenti di SQL Server 2016 può migliorare chiaramente le esecuzioni delle query. È un dato di fatto. Come qualsiasi nuova funzionalità, naturalmente, una corretta valutazione deve essere effettuata toodetermine hello esattamente le condizioni in cui il carico di lavoro del database funziona meglio hello. Esperienza mostra che la maggior parte delle carico di lavoro sono tooat previsto almeno eseguiti in modo trasparente il livello di compatibilità 130, sfruttando la nuova query di elaborazione, funzioni e nuova stima della cardinalità. Ovvero Ciò premesso, in realtà, sono sempre presenti alcune eccezioni e l'esecuzione di scadenza appropriata molta attenzione toodetermine una valutazione importante quanto è possibile trarre vantaggio da tali miglioramenti. E nuovamente, archivio Query hello può essere di grande aiuto in questo modo.

Come si evolve SQL Azure, è possibile prevedere un livello di compatibilità 140 in hello future. Al momento opportuno verranno trattate anche le nuove caratteristiche del futuro livello di compatibilità 140, come si è fatto brevemente in questo articolo per il livello di compatibilità 130.

Per il momento opportuno non dimenticare, a partire da giugno 2016, Database SQL di Azure passerà il livello di compatibilità predefinito hello da 120 too130 per i database appena creati. Tenere presente questa informazione.

## <a name="references"></a>Riferimenti
* [Novità (Motore di database)](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [Post di blog: Archivio query, la scatola nera del database, di Borko Novakovic, 8 giugno 2016](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [Livello di compatibilità ALTER TABLE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)
* [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](https://msdn.microsoft.com/library/mt629158.aspx)
* [Livello di compatibilità 130 per il database SQL di Azure versione 12](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [Ottimizzazione del piani di Query con hello stima della cardinalità di SQL Server 2014](https://msdn.microsoft.com/library/dn673537.aspx)
* [Descrizione degli indici columnstore](https://msdn.microsoft.com/library/gg492088.aspx)
* [Post di blog: Miglioramento delle prestazioni delle query con il livello di compatibilità 130 nel database SQL di Azure, di Alain Lissoir, 6 maggio 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
