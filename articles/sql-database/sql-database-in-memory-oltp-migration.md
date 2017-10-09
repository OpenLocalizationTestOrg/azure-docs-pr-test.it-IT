---
title: OLTP in memoria di aaaIn migliora le prestazioni SQL txn | Documenti Microsoft
description: OLTP In memoria adottino tooimprove transazionale delle prestazioni in un database SQL esistente.
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a><span data-ttu-id="932bb-103">OLTP In memoria utilizzare tooimprove le prestazioni dell'applicazione nel Database SQL</span><span class="sxs-lookup"><span data-stu-id="932bb-103">Use In-Memory OLTP tooimprove your application performance in SQL Database</span></span>
<span data-ttu-id="932bb-104">[OLTP in memoria](sql-database-in-memory.md) può essere utilizzato tooimprove hello prestazioni di elaborazione delle transazioni, inserimento di dati e gli scenari di dati temporanei, in [Premium](sql-database-service-tiers.md) database SQL di Azure senza aumentare hello piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="932bb-104">[In-Memory OLTP](sql-database-in-memory.md) can be used tooimprove hello performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing hello pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="932bb-105">Informazioni in [Quorum doubles key database's workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database) (Il quorum raddoppia il carico di lavoro del database principale riducendo il DTU del 70% con il database SQL)</span><span class="sxs-lookup"><span data-stu-id="932bb-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="932bb-106">Seguire questi passaggi tooadopt OLTP In memoria, nel database esistente.</span><span class="sxs-lookup"><span data-stu-id="932bb-106">Follow these steps tooadopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="932bb-107">Passaggio 1: assicurarsi di usare un database Premium</span><span class="sxs-lookup"><span data-stu-id="932bb-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="932bb-108">OLTP in memoria è supportato solo nei database Premium.</span><span class="sxs-lookup"><span data-stu-id="932bb-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="932bb-109">In memoria è supportata se hello ha restituito il risultato è 1 (non 0):</span><span class="sxs-lookup"><span data-stu-id="932bb-109">In-Memory is supported if hello returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="932bb-110">*XTP* è l'acronimo di *Extreme Transaction Processing*</span><span class="sxs-lookup"><span data-stu-id="932bb-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a><span data-ttu-id="932bb-111">Passaggio 2: Identificare gli oggetti toomigrate tooIn memoria OLTP</span><span class="sxs-lookup"><span data-stu-id="932bb-111">Step 2: Identify objects toomigrate tooIn-Memory OLTP</span></span>
<span data-ttu-id="932bb-112">SSMS include un report **Panoramica analisi delle prestazioni per le transazioni** che è possibile eseguire su un database con un carico di lavoro attivo.</span><span class="sxs-lookup"><span data-stu-id="932bb-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="932bb-113">report di Hello identifica le tabelle e stored procedure candidate per la migrazione OLTP in memoria di tooIn.</span><span class="sxs-lookup"><span data-stu-id="932bb-113">hello report identifies tables and stored procedures that are candidates for migration tooIn-Memory OLTP.</span></span>

<span data-ttu-id="932bb-114">In SSMS, report hello toogenerate:</span><span class="sxs-lookup"><span data-stu-id="932bb-114">In SSMS, toogenerate hello report:</span></span>

* <span data-ttu-id="932bb-115">In hello **Esplora oggetti**, fare doppio clic sul nodo del database.</span><span class="sxs-lookup"><span data-stu-id="932bb-115">In hello **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="932bb-116">Fare clic su **Report** > **Report standard** > **Panoramica dell'analisi delle prestazioni transazioni**.</span><span class="sxs-lookup"><span data-stu-id="932bb-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="932bb-117">Per ulteriori informazioni, vedere [determinare se una tabella o una Stored Procedure deve essere trasferita OLTP in memoria di tooIn](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="932bb-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="932bb-118">Passaggio 3: Creare un database di prova confrontabile</span><span class="sxs-lookup"><span data-stu-id="932bb-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="932bb-119">Si supponga che il report hello indica il database è una tabella che può costituire un vantaggio viene convertita tooa nella tabella con ottimizzazione per la memoria.</span><span class="sxs-lookup"><span data-stu-id="932bb-119">Suppose hello report indicates your database has a table that would benefit from being converted tooa memory-optimized table.</span></span> <span data-ttu-id="932bb-120">È consigliabile testare indicazione hello tooconfirm eseguendo i test.</span><span class="sxs-lookup"><span data-stu-id="932bb-120">We recommend that you first test tooconfirm hello indication by testing.</span></span>

<span data-ttu-id="932bb-121">È necessaria una copia di test del database di produzione.</span><span class="sxs-lookup"><span data-stu-id="932bb-121">You need a test copy of your production database.</span></span> <span data-ttu-id="932bb-122">Hello database di test deve essere in hello stesso servizio livello del database di produzione.</span><span class="sxs-lookup"><span data-stu-id="932bb-122">hello test database should be at hello same service tier level as your production database.</span></span>

<span data-ttu-id="932bb-123">tooease test, modificare il database di test come segue:</span><span class="sxs-lookup"><span data-stu-id="932bb-123">tooease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="932bb-124">Connettersi toohello test database tramite SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="932bb-124">Connect toohello test database by using SSMS.</span></span>
2. <span data-ttu-id="932bb-125">tooavoid necessità hello opzione WITH (SNAPSHOT) nelle query, impostare l'opzione di database hello come illustrato nella seguente istruzione T-SQL hello:</span><span class="sxs-lookup"><span data-stu-id="932bb-125">tooavoid needing hello WITH (SNAPSHOT) option in queries, set hello database option as shown in hello following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="932bb-126">Passaggio 4: Eseguire la migrazione delle tabelle</span><span class="sxs-lookup"><span data-stu-id="932bb-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="932bb-127">È necessario creare e popolare una copia con ottimizzazione per la memoria della tabella hello desiderato tootest.</span><span class="sxs-lookup"><span data-stu-id="932bb-127">You must create and populate a memory-optimized copy of hello table you want tootest.</span></span> <span data-ttu-id="932bb-128">È possibile crearla usando:</span><span class="sxs-lookup"><span data-stu-id="932bb-128">You can create it by using either:</span></span>

* <span data-ttu-id="932bb-129">Hello utile memoria Ottimizzazione guidata in SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="932bb-129">hello handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="932bb-130">T-SQL manuale.</span><span class="sxs-lookup"><span data-stu-id="932bb-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="932bb-131">Ottimizzazione guidata per la memoria di SSMS</span><span class="sxs-lookup"><span data-stu-id="932bb-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="932bb-132">toouse questa opzione di migrazione:</span><span class="sxs-lookup"><span data-stu-id="932bb-132">toouse this migration option:</span></span>

1. <span data-ttu-id="932bb-133">Connettere il database di prova toohello con SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="932bb-133">Connect toohello test database with SSMS.</span></span>
2. <span data-ttu-id="932bb-134">In hello **Esplora oggetti**, fare clic su tabella hello e quindi fare clic su **Memory Optimization Advisor**.</span><span class="sxs-lookup"><span data-stu-id="932bb-134">In hello **Object Explorer**, right-click on hello table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="932bb-135">Hello **tabella memoria Query Optimizer Advisor** procedura guidata viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="932bb-135">hello **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="932bb-136">Nella procedura guidata hello, fare clic su **convalida migrazione** (o hello **Avanti** pulsante) toosee se la tabella hello contiene funzionalità non supportate che non sono supportate nelle tabelle con ottimizzazione per la memoria.</span><span class="sxs-lookup"><span data-stu-id="932bb-136">In hello wizard, click **Migration validation** (or hello **Next** button) toosee if hello table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="932bb-137">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="932bb-137">For more information, see:</span></span>
   
   * <span data-ttu-id="932bb-138">Hello *checklist Ottimizzazione memoria* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="932bb-138">hello *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="932bb-139">[Costrutti transact-SQL non supportati da OLTP in memoria](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="932bb-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="932bb-140">[Migrazione OLTP in memoria di tooIn](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="932bb-140">[Migrating tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="932bb-141">Se la tabella hello non dispone di funzionalità supportate, advisor hello eseguibili schema effettivo hello e la migrazione dei dati per l'utente.</span><span class="sxs-lookup"><span data-stu-id="932bb-141">If hello table has no unsupported features, hello advisor can perform hello actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="932bb-142">T-SQL manuale</span><span class="sxs-lookup"><span data-stu-id="932bb-142">Manual T-SQL</span></span>
<span data-ttu-id="932bb-143">toouse questa opzione di migrazione:</span><span class="sxs-lookup"><span data-stu-id="932bb-143">toouse this migration option:</span></span>

1. <span data-ttu-id="932bb-144">Connettersi tooyour test database tramite SQL Server Management Studio (o un'utilità analoga).</span><span class="sxs-lookup"><span data-stu-id="932bb-144">Connect tooyour test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="932bb-145">Ottenere script T-SQL completo hello per la tabella e i relativi indici.</span><span class="sxs-lookup"><span data-stu-id="932bb-145">Obtain hello complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="932bb-146">In SSMS fare clic con il pulsante destro del mouse sul nodo della tabella.</span><span class="sxs-lookup"><span data-stu-id="932bb-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="932bb-147">Fare clic su **Crea script per tabella** > **CREATE in** > **Nuova finestra Query**.</span><span class="sxs-lookup"><span data-stu-id="932bb-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="932bb-148">Nella finestra di script hello, aggiungere WITH (MEMORY_OPTIMIZED = ON) toohello istruzione CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="932bb-148">In hello script window, add WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE statement.</span></span>
4. <span data-ttu-id="932bb-149">Se è presente un indice cluster, modificare tooNONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="932bb-149">If there is a CLUSTERED index, change it tooNONCLUSTERED.</span></span>
5. <span data-ttu-id="932bb-150">Rinominare la tabella esistente hello tramite SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="932bb-150">Rename hello existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="932bb-151">Creare hello con ottimizzazione per la memoria copia della tabella hello eseguendo lo script CREATE TABLE modificato.</span><span class="sxs-lookup"><span data-stu-id="932bb-151">Create hello new memory-optimized copy of hello table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="932bb-152">Copia una tabella con ottimizzazione per la memoria di hello dati tooyour utilizzando l'istruzione INSERT... SELEZIONARE * IN:</span><span class="sxs-lookup"><span data-stu-id="932bb-152">Copy hello data tooyour memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="932bb-153">Passaggio 5 (facoltativo): Eseguire la migrazione di stored procedure</span><span class="sxs-lookup"><span data-stu-id="932bb-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="932bb-154">funzionalità In memoria Hello è inoltre possibile modificare una stored procedure per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="932bb-154">hello In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="932bb-155">Considerazioni sulle stored procedure compilate in modo nativo</span><span class="sxs-lookup"><span data-stu-id="932bb-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="932bb-156">Una stored procedure compilata in modo nativo deve avere hello nella relativa clausola T-SQL con le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="932bb-156">A natively compiled stored procedure must have hello following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="932bb-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="932bb-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="932bb-158">SCHEMABINDING: tabelle significato hello stored procedure non possono contenere definizioni di colonna modificate in alcun modo che hanno effetto sulla procedura hello archiviato, a meno che non si rilascia di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="932bb-158">SCHEMABINDING: meaning tables that hello stored procedure cannot have their column definitions changed in any way that would affect hello stored procedure, unless you drop hello stored procedure.</span></span>

<span data-ttu-id="932bb-159">Un modulo nativo deve usare [blocchi ATOMICI](http://msdn.microsoft.com/library/dn452281.aspx) di grandi dimensioni per la gestione delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="932bb-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="932bb-160">Non esiste un ruolo per un'istruzione BEGIN TRANSACTION o ROLLBACK TRANSACTION esplicita.</span><span class="sxs-lookup"><span data-stu-id="932bb-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="932bb-161">Se viene rilevata una violazione di una regola business, è possibile terminare il blocco atomico hello con un [generare](http://msdn.microsoft.com/library/ee677615.aspx) istruzione.</span><span class="sxs-lookup"><span data-stu-id="932bb-161">If your code detects a violation of a business rule, it can terminate hello atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="932bb-162">CREATE PROCEDURE tipica per le stored procedure compilate in modo nativo</span><span class="sxs-lookup"><span data-stu-id="932bb-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="932bb-163">In genere hello T-SQL toocreate una stored procedure compilata in modo nativo è simile toohello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="932bb-163">Typically hello T-SQL toocreate a natively compiled stored procedure is similar toohello following template:</span></span>

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* <span data-ttu-id="932bb-164">Per hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT è di hello più comuni valore per hello compilata in modo nativo stored procedura.</span><span class="sxs-lookup"><span data-stu-id="932bb-164">For hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is hello most common value for hello natively compiled stored procedure.</span></span> <span data-ttu-id="932bb-165">Tuttavia, un subset di hello altri valori sono inoltre supportati:</span><span class="sxs-lookup"><span data-stu-id="932bb-165">However,  a subset of hello other values are also supported:</span></span>
  
  * <span data-ttu-id="932bb-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="932bb-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="932bb-167">SERIALIZABLE</span><span class="sxs-lookup"><span data-stu-id="932bb-167">SERIALIZABLE</span></span>
* <span data-ttu-id="932bb-168">Hello valore lingua deve essere presente nella visualizzazione sys.languages hello.</span><span class="sxs-lookup"><span data-stu-id="932bb-168">hello LANGUAGE value must be present in hello sys.languages view.</span></span>

### <a name="how-toomigrate-a-stored-procedure"></a><span data-ttu-id="932bb-169">Come toomigrate una stored procedure</span><span class="sxs-lookup"><span data-stu-id="932bb-169">How toomigrate a stored procedure</span></span>
<span data-ttu-id="932bb-170">i passaggi della migrazione Hello sono:</span><span class="sxs-lookup"><span data-stu-id="932bb-170">hello migration steps are:</span></span>

1. <span data-ttu-id="932bb-171">Ottenere hello CREATE PROCEDURE script toohello stored procedure interpretata regolarmente.</span><span class="sxs-lookup"><span data-stu-id="932bb-171">Obtain hello CREATE PROCEDURE script toohello regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="932bb-172">Riscrivere il relativo modello di intestazione toomatch hello precedente.</span><span class="sxs-lookup"><span data-stu-id="932bb-172">Rewrite its header toomatch hello previous template.</span></span>
3. <span data-ttu-id="932bb-173">Verificare se la procedura hello archiviato codice T-SQL utilizza le caratteristiche che non sono supportate per le stored procedure compilate in modo nativo.</span><span class="sxs-lookup"><span data-stu-id="932bb-173">Ascertain whether hello stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="932bb-174">Se necessario, implementare le soluzioni alternative.</span><span class="sxs-lookup"><span data-stu-id="932bb-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="932bb-175">Per altre informazioni vedere [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="932bb-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="932bb-176">Rinominare una stored procedure precedente hello tramite SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="932bb-176">Rename hello old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="932bb-177">In alternativa usare semplicemente DROP.</span><span class="sxs-lookup"><span data-stu-id="932bb-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="932bb-178">Eseguire lo script CREATE PROCEDURE T-SQL modificato.</span><span class="sxs-lookup"><span data-stu-id="932bb-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="932bb-179">Passaggio 6: Eseguire il carico di lavoro nel test</span><span class="sxs-lookup"><span data-stu-id="932bb-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="932bb-180">Eseguire un carico di lavoro nel database di test di carico di lavoro toohello simile che viene eseguito nel database di produzione.</span><span class="sxs-lookup"><span data-stu-id="932bb-180">Run a workload in your test database that is similar toohello workload that runs in your production database.</span></span> <span data-ttu-id="932bb-181">Si rivelano miglioramento delle prestazioni hello ottenuto per l'utilizzo della funzionalità In memoria hello per le tabelle e stored procedure.</span><span class="sxs-lookup"><span data-stu-id="932bb-181">This should reveal hello performance gain achieved by your use of hello In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="932bb-182">Gli attributi principali di carico di lavoro hello sono:</span><span class="sxs-lookup"><span data-stu-id="932bb-182">Major attributes of hello workload are:</span></span>

* <span data-ttu-id="932bb-183">Numero di connessioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="932bb-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="932bb-184">Rapporto di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="932bb-184">Read/write ratio.</span></span>

<span data-ttu-id="932bb-185">tootailor e carico di lavoro di hello esecuzione dei test, è consigliabile usare uno strumento utile ostress.exe hello che illustrate nella [qui](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="932bb-185">tootailor and run hello test workload, consider using hello handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="932bb-186">latenza di rete toominimize, eseguire il test in hello stessa area geografica Azure in cui è presente il database di hello.</span><span class="sxs-lookup"><span data-stu-id="932bb-186">toominimize network latency, run your test in hello same Azure geographic region where hello database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="932bb-187">Passaggio 7: Monitoraggio post-implementazione</span><span class="sxs-lookup"><span data-stu-id="932bb-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="932bb-188">Si consideri il monitoraggio di effetti sulle prestazioni di hello delle implementazioni In memoria nell'ambiente di produzione:</span><span class="sxs-lookup"><span data-stu-id="932bb-188">Consider monitoring hello performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="932bb-189">[Monitorare l'archiviazione in memoria](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="932bb-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="932bb-190">Monitoraggio del database SQL di Azure tramite le visualizzazioni di gestione dinamica</span><span class="sxs-lookup"><span data-stu-id="932bb-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="932bb-191">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="932bb-191">Related links</span></span>
* [<span data-ttu-id="932bb-192">OLTP in memoria (ottimizzazione in memoria)</span><span class="sxs-lookup"><span data-stu-id="932bb-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="932bb-193">Introduzione tooNatively Compiled Stored Procedures</span><span class="sxs-lookup"><span data-stu-id="932bb-193">Introduction tooNatively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="932bb-194">Ottimizzazione guidata per la memoria</span><span class="sxs-lookup"><span data-stu-id="932bb-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

