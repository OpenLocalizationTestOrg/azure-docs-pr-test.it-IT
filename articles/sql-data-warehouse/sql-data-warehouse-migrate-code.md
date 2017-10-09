---
title: aaaMigrate il tooSQL codice SQL Data Warehouse | Documenti Microsoft
description: Suggerimenti per la migrazione del database SQL di codice tooAzure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 19c252a3-0e41-4eec-9d3e-09a68c7e7add
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/23/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 7a16d579d068e9df9aba3dc61e4a09bcaa551588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a>Eseguire la migrazione del tooSQL codice SQL Data Warehouse
Questo articolo illustra le modifiche al codice sarà probabilmente necessario toomake durante la migrazione del codice da un altro database tooSQL Data Warehouse. Alcune funzionalità di SQL Data Warehouse può migliorare significativamente le prestazioni come se fossero toowork progettato in modalità distribuita. Tuttavia, scalabilità e prestazioni di toomaintain, alcune funzionalità anche non sono disponibili.

## <a name="common-t-sql-limitations"></a>Limitazioni comuni di T-SQL
Hello seguente elenco di vengono riepilogate le funzionalità più comuni hello SQL Data Warehouse non è supportata. Hello collegamenti è possibile tooworkarounds per le funzionalità di hello non supportato:

* [Join ANSI sugli aggiornamenti][ANSI joins on updates]
* [Join ANSI sulle eliminazioni][ANSI joins on deletes]
* [Istruzione merge][merge statement]
* Join tra database
* [Cursori][cursors]
* <seg>
  [INSERT..EXEC][INSERT..EXEC]</seg>
* Clausola di output
* Funzioni inline definite dall'utente
* Funzioni a istruzioni multiple
* [espressioni di tabella comune](#Common-table-expressions)
* [espressioni tabella comune ricorsive (CTE)] (#Recursive-common-table-expressions-(CTE)
* Funzioni e procedure CLR
* Funzione $partition
* Variabili di tabella
* Parametri di valori di tabella
* Transazioni distribuite
* Commit / rollback
* Transazione di salvataggio
* Contesti di esecuzione (EXECUTE AS)
* [Raggruppamento per clausola con opzioni di rollup/cubo/set di raggruppamento][group by clause with rollup / cube / grouping sets options]
* [Livelli di annidamento superiori a 8][nesting levels beyond 8]
* [Aggiornamento tramite visualizzazioni][updating through views]
* [Uso di select per l'assegnazione di variabili][use of select for variable assignment]
* [Nessun tipo di dati MAX per stringhe SQL dinamiche][no MAX data type for dynamic SQL strings]

Fortunatamente è possibile ovviare alla maggior parte di queste limitazioni. Negli articoli pertinenti sviluppo hello citati in precedenza, vengono fornite spiegazioni.

## <a name="supported-cte-features"></a>Funzionalità CTE supportate
Le espressioni di tabella comune (CTE) sono parzialmente supportate in SQL Data Warehouse.  Hello seguenti caratteristiche CTE è attualmente supportata:

* Un'espressione CTE può essere specificata in un'istruzione SELECT.
* Un'espressione CTE può essere specificata in un'istruzione CREATE VIEW.
* Un'espressione CTE può essere specificata in un'istruzione CREATE TABLE AS SELECT (CTAS).
* Un'espressione CTE può essere specificata in un'istruzione CREATE REMOTE TABLE AS SELECT (CRTAS).
* Un'espressione CTE può essere specificata in un'istruzione CREATE EXTERNAL TABLE AS SELECT (CETAS).
* È possibile fare riferimento a una tabella remota da un'espressione CTE.
* È possibile fare riferimento a una tabella esterna da un'espressione CTE.
* In un'espressione CTE possono essere definite più definizioni di query CTE.

## <a name="cte-limitations"></a>Limitazioni CTE
Le espressioni di tabella comune presentano alcune limitazioni in SQL Data Warehouse, tra cui:

* Un'espressione CTE deve essere seguita da una singola istruzione SELECT. Le istruzioni INSERT, UPDATE, DELETE e MERGE non sono supportate.
* Un'espressione di tabella comune che include riferimenti tooitself (ricorsiva espressione di tabella comune) non è supportata (vedere la sezione sottostante).
* Non è consentito specificare più di una clausola WITH in un'espressione CTE. Se, ad esempio, CTE_query_definition contiene una sottoquery, tale sottoquery non può contenere una clausola WITH annidata che definisce un'altra CTE.
* Una clausola ORDER BY non possa essere utilizzata nel hello elementi CTE_query_definition, tranne quando viene specificata una clausola TOP.
* Quando una CTE è utilizzata in un'istruzione che fa parte di un batch, l'istruzione di hello prima che deve essere seguita da un punto e virgola.
* Quando utilizzata in istruzioni preparate da sp_prepare, CTE comporteranno hello esattamente come altre istruzioni SELECT in PDW. Se, tuttavia, le CTE vengono utilizzate come parte di CETAS preparato da sp_prepare, comportamento hello possibile rinviare da SQL Server e altre istruzioni PDW dovuta hello associazione viene implementata per sp_prepare. Se l'opzione Seleziona riferimenti CTE è utilizzata una colonna di tipo non corretta che non esiste nella CTE, hello sp_prepare passerà senza rilevare l'errore hello ma hello verrà generato un errore durante la sp_execute invece.

## <a name="recursive-ctes"></a>CTE ricorsive
Le CTE ricorsive non sono supportate in SQL Data Warehouse.  la migrazione di Hello della CTE ricorsiva può essere complessa e la procedura ottimale di hello è toobreak in più passaggi. In genere, è possibile utilizzare un ciclo e popolare una tabella temporanea come è possibile scorrere le query provvisorio hello ricorsive. Una volta che viene popolata la tabella temporanea hello è quindi possibile restituire dati hello come un unico set di risultati. Un approccio simile è stato utilizzato toosolve `GROUP BY WITH CUBE` in hello [gruppo dalla clausola con rollup / cubo / imposta le opzioni di raggruppamento] [ group by clause with rollup / cube / grouping sets options] articolo.

## <a name="unsupported-system-functions"></a>Funzioni di sistema non supportate
Anche alcune funzioni di sistema non sono supportate. Vengono elencate alcune delle hello principali dei quali che è possibile in genere utilizzato nel data warehouse

* NEWSEQUENTIALID()
* @@NESTLEVEL()
* @@IDENTITY()
* @@ROWCOUNT()
* ROWCOUNT_BIG
* ERROR_LINE()

Per alcuni di questi problemi esiste una soluzione alternativa.

## <a name="rowcount-workaround"></a>Soluzione alternativa @@ROWCOUNT
toowork intorno mancanza di supporto per @@ROWCOUNT, creare una stored procedure che recupererà hello ultimo conteggio delle righe da sys.dm_pdw_request_steps e quindi eseguire `EXEC LastRowCount` dopo un'istruzione DML.

```sql
CREATE PROCEDURE LastRowCount AS
WITH LastRequest as 
(   SELECT TOP 1    request_id
    FROM            sys.dm_pdw_exec_requests
    WHERE           session_id = SESSION_ID()
    AND             resource_class IS NOT NULL
    ORDER BY end_time DESC
),
LastRequestRowCounts as
(
    SELECT  step_index, row_count
    FROM    sys.dm_pdw_request_steps
    WHERE   row_count >= 0
    AND     request_id IN (SELECT request_id from LastRequest)
)
SELECT TOP 1 row_count FROM LastRequestRowCounts ORDER BY step_index DESC
;
```

## <a name="next-steps"></a>Passaggi successivi
Per un elenco completo di tutte le istruzioni T-SQL supportate, vedere [Argomenti Transact-SQL][Transact-SQL topics].

<!--Image references-->

<!--Article references-->
[ANSI joins on updates]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[ANSI joins on deletes]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[merge statement]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[INSERT..EXEC]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[Transact-SQL topics]: ./sql-data-warehouse-reference-tsql-statements.md

[cursors]: ./sql-data-warehouse-develop-loops.md
[group by clause with rollup / cube / grouping sets options]: ./sql-data-warehouse-develop-group-by-options.md
[nesting levels beyond 8]: ./sql-data-warehouse-develop-transactions.md
[updating through views]: ./sql-data-warehouse-develop-views.md
[use of select for variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[no MAX data type for dynamic SQL strings]: ./sql-data-warehouse-develop-dynamic-sql.md

<!--MSDN references-->

<!--Other Web references-->
