---
title: Eseguire la migrazione del codice SQL in SQL Data Warehouse | Documentazione Microsoft
description: Suggerimenti per la migrazione del codice SQL in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
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
ms.openlocfilehash: c6e6b890f5e2d0e31b10bbb6803adad02bf60248
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-sql-code-to-sql-data-warehouse"></a><span data-ttu-id="41378-103">Eseguire la migrazione del codice SQL in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="41378-103">Migrate your SQL code to SQL Data Warehouse</span></span>
<span data-ttu-id="41378-104">Questo articolo spiega le modifiche del codice che saranno molto probabilmente necessarie quando si esegue la migrazione del codice da un altro database in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="41378-104">This article explains code changes you will probably need to make when migrating your code from another database to SQL Data Warehouse.</span></span> <span data-ttu-id="41378-105">Alcune funzionalità di SQL Data Warehouse possono migliorare in modo significativo le prestazioni perché sono progettate per funzionare direttamente in modalità distribuita.</span><span class="sxs-lookup"><span data-stu-id="41378-105">Some SQL Data Warehouse features can significantly improve performance as they are designed to work in a distributed fashion.</span></span> <span data-ttu-id="41378-106">Per mantenere tuttavia le prestazioni e la scalabilità, alcune funzionalità non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="41378-106">However, to maintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="41378-107">Limitazioni comuni di T-SQL</span><span class="sxs-lookup"><span data-stu-id="41378-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="41378-108">L'elenco seguente riepiloga le funzionalità più comuni non supportate in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="41378-108">The following list summarizes the most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="41378-109">I collegamenti consentono di accedere a soluzioni alternative per le funzionalità non supportate:</span><span class="sxs-lookup"><span data-stu-id="41378-109">The links take you to workarounds for the unsupported features:</span></span>

* <span data-ttu-id="41378-110">[Join ANSI sugli aggiornamenti][ANSI joins on updates]</span><span class="sxs-lookup"><span data-stu-id="41378-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="41378-111">[Join ANSI sulle eliminazioni][ANSI joins on deletes]</span><span class="sxs-lookup"><span data-stu-id="41378-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="41378-112">[Istruzione merge][merge statement]</span><span class="sxs-lookup"><span data-stu-id="41378-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="41378-113">Join tra database</span><span class="sxs-lookup"><span data-stu-id="41378-113">cross-database joins</span></span>
* <span data-ttu-id="41378-114">[Cursori][cursors]</span><span class="sxs-lookup"><span data-stu-id="41378-114">[cursors][cursors]</span></span>
* <span data-ttu-id="41378-115"><seg>
  [INSERT..EXEC][INSERT..EXEC]</seg></span><span class="sxs-lookup"><span data-stu-id="41378-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="41378-116">Clausola di output</span><span class="sxs-lookup"><span data-stu-id="41378-116">output clause</span></span>
* <span data-ttu-id="41378-117">Funzioni inline definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="41378-117">inline user-defined functions</span></span>
* <span data-ttu-id="41378-118">Funzioni a istruzioni multiple</span><span class="sxs-lookup"><span data-stu-id="41378-118">multi-statement functions</span></span>
* [<span data-ttu-id="41378-119">espressioni di tabella comune</span><span class="sxs-lookup"><span data-stu-id="41378-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="41378-120">[espressioni tabella comune ricorsive (CTE)] (#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="41378-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="41378-121">Funzioni e procedure CLR</span><span class="sxs-lookup"><span data-stu-id="41378-121">CLR functions and procedures</span></span>
* <span data-ttu-id="41378-122">Funzione $partition</span><span class="sxs-lookup"><span data-stu-id="41378-122">$partition function</span></span>
* <span data-ttu-id="41378-123">Variabili di tabella</span><span class="sxs-lookup"><span data-stu-id="41378-123">table variables</span></span>
* <span data-ttu-id="41378-124">Parametri di valori di tabella</span><span class="sxs-lookup"><span data-stu-id="41378-124">table value parameters</span></span>
* <span data-ttu-id="41378-125">Transazioni distribuite</span><span class="sxs-lookup"><span data-stu-id="41378-125">distributed transactions</span></span>
* <span data-ttu-id="41378-126">Commit / rollback</span><span class="sxs-lookup"><span data-stu-id="41378-126">commit / rollback work</span></span>
* <span data-ttu-id="41378-127">Transazione di salvataggio</span><span class="sxs-lookup"><span data-stu-id="41378-127">save transaction</span></span>
* <span data-ttu-id="41378-128">Contesti di esecuzione (EXECUTE AS)</span><span class="sxs-lookup"><span data-stu-id="41378-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="41378-129">[Raggruppamento per clausola con opzioni di rollup/cubo/set di raggruppamento][group by clause with rollup / cube / grouping sets options]</span><span class="sxs-lookup"><span data-stu-id="41378-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="41378-130">[Livelli di annidamento superiori a 8][nesting levels beyond 8]</span><span class="sxs-lookup"><span data-stu-id="41378-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="41378-131">[Aggiornamento tramite visualizzazioni][updating through views]</span><span class="sxs-lookup"><span data-stu-id="41378-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="41378-132">[Uso di select per l'assegnazione di variabili][use of select for variable assignment]</span><span class="sxs-lookup"><span data-stu-id="41378-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="41378-133">[Nessun tipo di dati MAX per stringhe SQL dinamiche][no MAX data type for dynamic SQL strings]</span><span class="sxs-lookup"><span data-stu-id="41378-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="41378-134">Fortunatamente è possibile ovviare alla maggior parte di queste limitazioni.</span><span class="sxs-lookup"><span data-stu-id="41378-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="41378-135">Le spiegazioni sono fornite dagli articoli pertinenti a cui viene fatto riferimento più indietro.</span><span class="sxs-lookup"><span data-stu-id="41378-135">Explanations are provided in the relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="41378-136">Funzionalità CTE supportate</span><span class="sxs-lookup"><span data-stu-id="41378-136">Supported CTE features</span></span>
<span data-ttu-id="41378-137">Le espressioni di tabella comune (CTE) sono parzialmente supportate in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="41378-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="41378-138">Attualmente sono supportate le funzionalità CTE seguenti:</span><span class="sxs-lookup"><span data-stu-id="41378-138">The following CTE features are currently supported:</span></span>

* <span data-ttu-id="41378-139">Un'espressione CTE può essere specificata in un'istruzione SELECT.</span><span class="sxs-lookup"><span data-stu-id="41378-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="41378-140">Un'espressione CTE può essere specificata in un'istruzione CREATE VIEW.</span><span class="sxs-lookup"><span data-stu-id="41378-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="41378-141">Un'espressione CTE può essere specificata in un'istruzione CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="41378-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="41378-142">Un'espressione CTE può essere specificata in un'istruzione CREATE REMOTE TABLE AS SELECT (CRTAS).</span><span class="sxs-lookup"><span data-stu-id="41378-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="41378-143">Un'espressione CTE può essere specificata in un'istruzione CREATE EXTERNAL TABLE AS SELECT (CETAS).</span><span class="sxs-lookup"><span data-stu-id="41378-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="41378-144">È possibile fare riferimento a una tabella remota da un'espressione CTE.</span><span class="sxs-lookup"><span data-stu-id="41378-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="41378-145">È possibile fare riferimento a una tabella esterna da un'espressione CTE.</span><span class="sxs-lookup"><span data-stu-id="41378-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="41378-146">In un'espressione CTE possono essere definite più definizioni di query CTE.</span><span class="sxs-lookup"><span data-stu-id="41378-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="41378-147">Limitazioni CTE</span><span class="sxs-lookup"><span data-stu-id="41378-147">CTE Limitations</span></span>
<span data-ttu-id="41378-148">Le espressioni di tabella comune presentano alcune limitazioni in SQL Data Warehouse, tra cui:</span><span class="sxs-lookup"><span data-stu-id="41378-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="41378-149">Un'espressione CTE deve essere seguita da una singola istruzione SELECT.</span><span class="sxs-lookup"><span data-stu-id="41378-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="41378-150">Le istruzioni INSERT, UPDATE, DELETE e MERGE non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="41378-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="41378-151">Un'espressione di tabella comune che include riferimenti a se stessa (un'espressione di tabella comune ricorsiva) non è supportata (vedere la sezione sotto).</span><span class="sxs-lookup"><span data-stu-id="41378-151">A common table expression that includes references to itself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="41378-152">Non è consentito specificare più di una clausola WITH in un'espressione CTE.</span><span class="sxs-lookup"><span data-stu-id="41378-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="41378-153">Se, ad esempio, CTE_query_definition contiene una sottoquery, tale sottoquery non può contenere una clausola WITH annidata che definisce un'altra CTE.</span><span class="sxs-lookup"><span data-stu-id="41378-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="41378-154">Una clausola ORDER BY non può essere usata in CTE_query_definition, tranne quando viene specificata una clausola TOP.</span><span class="sxs-lookup"><span data-stu-id="41378-154">An ORDER BY clause cannot be used in the CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="41378-155">Quando un'espressione CTE viene usata in un'istruzione che fa parte di un batch, l'istruzione precedente deve essere seguita da un punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="41378-155">When a CTE is used in a statement that is part of a batch, the statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="41378-156">Quando vengono usate in istruzioni preparate da sp_prepare, le espressioni CTE si comporteranno esattamente come le altre istruzioni SELECT in PDW.</span><span class="sxs-lookup"><span data-stu-id="41378-156">When used in statements prepared by sp_prepare, CTEs will behave the same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="41378-157">Tuttavia, se le CTE vengono usate come parte di istruzioni CETAS preparate da sp_prepare, il comportamento può variare rispetto a SQL Server e altre istruzioni PDW per la modalità di implementazione del binding per sp_prepare.</span><span class="sxs-lookup"><span data-stu-id="41378-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, the behavior can defer from SQL Server and other PDW statements because of the way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="41378-158">Se l'istruzione SELECT che fa riferimento alla CTE usa una colonna non corretta che non esiste nella CTE, sp_prepare passa senza rilevare l'errore, che invece viene generato durante sp_execute.</span><span class="sxs-lookup"><span data-stu-id="41378-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, the sp_prepare will pass without detecting the error, but the error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="41378-159">CTE ricorsive</span><span class="sxs-lookup"><span data-stu-id="41378-159">Recursive CTEs</span></span>
<span data-ttu-id="41378-160">Le CTE ricorsive non sono supportate in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="41378-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="41378-161">La migrazione di CTE ricorsive può essere complessa e il processo ottimale consiste nel suddividere l'operazione in più passaggi.</span><span class="sxs-lookup"><span data-stu-id="41378-161">The migration of recursive CTE can be somewhat complex and the best process is to break it into multiple steps.</span></span> <span data-ttu-id="41378-162">In genere è possibile usare un ciclo e popolare una tabella temporanea mentre si scorrono le query provvisorie ricorsive.</span><span class="sxs-lookup"><span data-stu-id="41378-162">You can typically use a loop and populate a temporary table as you iterate over the recursive interim queries.</span></span> <span data-ttu-id="41378-163">Una volta che viene popolata la tabella temporanea, è quindi possibile restituire i dati come un unico set di risultati.</span><span class="sxs-lookup"><span data-stu-id="41378-163">Once the temporary table is populated you can then return the data as a single result set.</span></span> <span data-ttu-id="41378-164">Un approccio simile è stato usato per risolvere `GROUP BY WITH CUBE` nell'articolo relativo al [raggruppamento per clausola con opzioni di rollup/cubo/set di raggruppamento][group by clause with rollup / cube / grouping sets options].</span><span class="sxs-lookup"><span data-stu-id="41378-164">A similar approach has been used to solve `GROUP BY WITH CUBE` in the [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="41378-165">Funzioni di sistema non supportate</span><span class="sxs-lookup"><span data-stu-id="41378-165">Unsupported system functions</span></span>
<span data-ttu-id="41378-166">Anche alcune funzioni di sistema non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="41378-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="41378-167">Alcune di queste funzioni principali che in genere vengono usate nel data warehousing sono:</span><span class="sxs-lookup"><span data-stu-id="41378-167">Some of the main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="41378-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="41378-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="41378-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="41378-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="41378-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="41378-170">@@IDENTITY()</span></span>
* <span data-ttu-id="41378-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="41378-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="41378-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="41378-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="41378-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="41378-173">ERROR_LINE()</span></span>

<span data-ttu-id="41378-174">Per alcuni di questi problemi esiste una soluzione alternativa.</span><span class="sxs-lookup"><span data-stu-id="41378-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="41378-175">Soluzione alternativa @@ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="41378-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="41378-176">Per risolvere la mancanza di supporto per @@ROWCOUNT, creare una stored procedure per recuperare l'ultimo conteggio delle righe da sys.dm_pdw_request_steps e quindi eseguire `EXEC LastRowCount` dopo un'istruzione DML.</span><span class="sxs-lookup"><span data-stu-id="41378-176">To work around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve the last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="41378-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="41378-177">Next steps</span></span>
<span data-ttu-id="41378-178">Per un elenco completo di tutte le istruzioni T-SQL supportate, vedere [Argomenti Transact-SQL][Transact-SQL topics].</span><span class="sxs-lookup"><span data-stu-id="41378-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

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
