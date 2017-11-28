---
title: OLTP in memoria migliora le prestazioni delle transazioni SQL | Documentazione Microsoft
description: Adottare OLTP in memoria per migliorare le prestazioni transazionali in un database SQL esistente.
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
ms.openlocfilehash: 50eed9aed417778bd497f55e20c8e732fdae9cf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-in-memory-oltp-to-improve-your-application-performance-in-sql-database"></a><span data-ttu-id="8de89-103">Uso di OLTP in memoria per migliorare le prestazioni delle applicazioni nel database SQL</span><span class="sxs-lookup"><span data-stu-id="8de89-103">Use In-Memory OLTP to improve your application performance in SQL Database</span></span>
<span data-ttu-id="8de89-104">[OLTP in memoria](sql-database-in-memory.md) può essere usato per migliorare le prestazioni di elaborazione delle transazioni, l'inserimento dei dati e gli scenari di dati temporanei, nei database SQL di Azure [Premium](sql-database-service-tiers.md), senza aumentare il piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="8de89-104">[In-Memory OLTP](sql-database-in-memory.md) can be used to improve the performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing the pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="8de89-105">Informazioni in [Quorum doubles key database's workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database) (Il quorum raddoppia il carico di lavoro del database principale riducendo il DTU del 70% con il database SQL)</span><span class="sxs-lookup"><span data-stu-id="8de89-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="8de89-106">Seguire i passaggi seguenti per adottare OLTP in memoria nel database esistente.</span><span class="sxs-lookup"><span data-stu-id="8de89-106">Follow these steps to adopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="8de89-107">Passaggio 1: assicurarsi di usare un database Premium</span><span class="sxs-lookup"><span data-stu-id="8de89-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="8de89-108">OLTP in memoria è supportato solo nei database Premium.</span><span class="sxs-lookup"><span data-stu-id="8de89-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="8de89-109">La funzionalità in memoria è supportata se il risultato restituito è 1 (non 0):</span><span class="sxs-lookup"><span data-stu-id="8de89-109">In-Memory is supported if the returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="8de89-110">*XTP* è l'acronimo di *Extreme Transaction Processing*</span><span class="sxs-lookup"><span data-stu-id="8de89-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-to-migrate-to-in-memory-oltp"></a><span data-ttu-id="8de89-111">Passaggio 2: Identificare gli oggetti per eseguire la migrazione a OLTP In memoria</span><span class="sxs-lookup"><span data-stu-id="8de89-111">Step 2: Identify objects to migrate to In-Memory OLTP</span></span>
<span data-ttu-id="8de89-112">SSMS include un report **Panoramica analisi delle prestazioni per le transazioni** che è possibile eseguire su un database con un carico di lavoro attivo.</span><span class="sxs-lookup"><span data-stu-id="8de89-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="8de89-113">Il report identifica le tabelle e le stored procedure candidate per la migrazione a OLTP in memoria.</span><span class="sxs-lookup"><span data-stu-id="8de89-113">The report identifies tables and stored procedures that are candidates for migration to In-Memory OLTP.</span></span>

<span data-ttu-id="8de89-114">In SSMS, per generare il report:</span><span class="sxs-lookup"><span data-stu-id="8de89-114">In SSMS, to generate the report:</span></span>

* <span data-ttu-id="8de89-115">In **Esplora oggetti**fare clic con il pulsante destro del mouse sul nodo del database.</span><span class="sxs-lookup"><span data-stu-id="8de89-115">In the **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="8de89-116">Fare clic su **Report** > **Report standard** > **Panoramica dell'analisi delle prestazioni transazioni**.</span><span class="sxs-lookup"><span data-stu-id="8de89-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="8de89-117">Per altre informazioni, vedere [Determinare se una tabella o una stored procedure deve essere trasferita a OLTP in memoria](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="8de89-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported to In-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="8de89-118">Passaggio 3: Creare un database di prova confrontabile</span><span class="sxs-lookup"><span data-stu-id="8de89-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="8de89-119">Si supponga che il report indichi che il database include una tabella che può trarre vantaggio dalla conversione in una tabella con ottimizzazione per la memoria.</span><span class="sxs-lookup"><span data-stu-id="8de89-119">Suppose the report indicates your database has a table that would benefit from being converted to a memory-optimized table.</span></span> <span data-ttu-id="8de89-120">È consigliabile verificare prima di tutto l'indicazione eseguendo il test.</span><span class="sxs-lookup"><span data-stu-id="8de89-120">We recommend that you first test to confirm the indication by testing.</span></span>

<span data-ttu-id="8de89-121">È necessaria una copia di test del database di produzione.</span><span class="sxs-lookup"><span data-stu-id="8de89-121">You need a test copy of your production database.</span></span> <span data-ttu-id="8de89-122">Il database di test deve avere lo stesso livello di servizio del database di produzione.</span><span class="sxs-lookup"><span data-stu-id="8de89-122">The test database should be at the same service tier level as your production database.</span></span>

<span data-ttu-id="8de89-123">Per semplificare il test, perfezionare il database di test come segue:</span><span class="sxs-lookup"><span data-stu-id="8de89-123">To ease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="8de89-124">Connettersi al database di test usando SSMS.</span><span class="sxs-lookup"><span data-stu-id="8de89-124">Connect to the test database by using SSMS.</span></span>
2. <span data-ttu-id="8de89-125">Per evitare di dover usare l'opzione WITH (SNAPSHOT) nelle query, impostare l'opzione di database come illustrato nell'istruzione T-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="8de89-125">To avoid needing the WITH (SNAPSHOT) option in queries, set the database option as shown in the following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="8de89-126">Passaggio 4: Eseguire la migrazione delle tabelle</span><span class="sxs-lookup"><span data-stu-id="8de89-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="8de89-127">È necessario creare e popolare una copia con ottimizzazione per la memoria della tabella che si vuole testare.</span><span class="sxs-lookup"><span data-stu-id="8de89-127">You must create and populate a memory-optimized copy of the table you want to test.</span></span> <span data-ttu-id="8de89-128">È possibile crearla usando:</span><span class="sxs-lookup"><span data-stu-id="8de89-128">You can create it by using either:</span></span>

* <span data-ttu-id="8de89-129">La pratica Ottimizzazione guidata per la memoria di SSMS.</span><span class="sxs-lookup"><span data-stu-id="8de89-129">The handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="8de89-130">T-SQL manuale.</span><span class="sxs-lookup"><span data-stu-id="8de89-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="8de89-131">Ottimizzazione guidata per la memoria di SSMS</span><span class="sxs-lookup"><span data-stu-id="8de89-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="8de89-132">Per usare questa opzione di migrazione:</span><span class="sxs-lookup"><span data-stu-id="8de89-132">To use this migration option:</span></span>

1. <span data-ttu-id="8de89-133">Connettersi al database di test con SSMS.</span><span class="sxs-lookup"><span data-stu-id="8de89-133">Connect to the test database with SSMS.</span></span>
2. <span data-ttu-id="8de89-134">In **Esplora oggetti** fare clic con il pulsante destro del mouse sulla tabella e quindi fare clic su **Ottimizzazione guidata per la memoria**.</span><span class="sxs-lookup"><span data-stu-id="8de89-134">In the **Object Explorer**, right-click on the table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="8de89-135">Verrà visualizzata l' **Ottimizzazione guidata per la memoria della tabella** .</span><span class="sxs-lookup"><span data-stu-id="8de89-135">The **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="8de89-136">Nella procedura guidata fare clic su **Convalida della migrazione** o sul pulsante **Avanti** per verificare se la tabella include eventuali funzionalità non supportate nelle tabelle con ottimizzazione per la memoria.</span><span class="sxs-lookup"><span data-stu-id="8de89-136">In the wizard, click **Migration validation** (or the **Next** button) to see if the table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="8de89-137">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="8de89-137">For more information, see:</span></span>
   
   * <span data-ttu-id="8de89-138">*Elenco di controllo relativo all'ottimizzazione per la memoria* in [Ottimizzazione guidata per la memoria](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="8de89-138">The *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="8de89-139">[Costrutti transact-SQL non supportati da OLTP in memoria](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="8de89-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="8de89-140">[Migrazione a OLTP in memoria](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="8de89-140">[Migrating to In-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="8de89-141">Se la tabella non include funzionalità non supportate, la procedura guidata può eseguire automaticamente la migrazione effettiva dello schema e dei dati.</span><span class="sxs-lookup"><span data-stu-id="8de89-141">If the table has no unsupported features, the advisor can perform the actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="8de89-142">T-SQL manuale</span><span class="sxs-lookup"><span data-stu-id="8de89-142">Manual T-SQL</span></span>
<span data-ttu-id="8de89-143">Per usare questa opzione di migrazione:</span><span class="sxs-lookup"><span data-stu-id="8de89-143">To use this migration option:</span></span>

1. <span data-ttu-id="8de89-144">Connettersi al database di test tramite SSMS o un'utilità analoga.</span><span class="sxs-lookup"><span data-stu-id="8de89-144">Connect to your test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="8de89-145">Ottenere lo script T-SQL completo per la tabella e i relativi indici.</span><span class="sxs-lookup"><span data-stu-id="8de89-145">Obtain the complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="8de89-146">In SSMS fare clic con il pulsante destro del mouse sul nodo della tabella.</span><span class="sxs-lookup"><span data-stu-id="8de89-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="8de89-147">Fare clic su **Crea script per tabella** > **CREATE in** > **Nuova finestra Query**.</span><span class="sxs-lookup"><span data-stu-id="8de89-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="8de89-148">Nella finestra dello script aggiungere WITH (MEMORY_OPTIMIZED = ON) all'istruzione CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="8de89-148">In the script window, add WITH (MEMORY_OPTIMIZED = ON) to the CREATE TABLE statement.</span></span>
4. <span data-ttu-id="8de89-149">Se esiste un indice CLUSTERED, modificarlo in NONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="8de89-149">If there is a CLUSTERED index, change it to NONCLUSTERED.</span></span>
5. <span data-ttu-id="8de89-150">Rinominare la tabella esistente in SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="8de89-150">Rename the existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="8de89-151">Creare la nuova copia della tabella con ottimizzazione per la memoria eseguendo lo script modificato CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="8de89-151">Create the new memory-optimized copy of the table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="8de89-152">Copiare i dati nella tabella con ottimizzazione per la memoria usando l'istruzione INSERT...SELECT * INTO:</span><span class="sxs-lookup"><span data-stu-id="8de89-152">Copy the data to your memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="8de89-153">Passaggio 5 (facoltativo): Eseguire la migrazione di stored procedure</span><span class="sxs-lookup"><span data-stu-id="8de89-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="8de89-154">La funzionalità in memoria può anche modificare una stored procedure per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="8de89-154">The In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="8de89-155">Considerazioni sulle stored procedure compilate in modo nativo</span><span class="sxs-lookup"><span data-stu-id="8de89-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="8de89-156">Una stored procedure compilata in modo nativo deve avere le opzioni seguenti nella relativa clausola WITH T-SQL:</span><span class="sxs-lookup"><span data-stu-id="8de89-156">A natively compiled stored procedure must have the following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="8de89-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="8de89-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="8de89-158">SCHEMABINDING: indica le tabelle in cui la stored procedure non può modificare le definizioni di colonna in alcun modo che abbia effetto sulla stored procedure, a meno che non si rimuova la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="8de89-158">SCHEMABINDING: meaning tables that the stored procedure cannot have their column definitions changed in any way that would affect the stored procedure, unless you drop the stored procedure.</span></span>

<span data-ttu-id="8de89-159">Un modulo nativo deve usare [blocchi ATOMICI](http://msdn.microsoft.com/library/dn452281.aspx) di grandi dimensioni per la gestione delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="8de89-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="8de89-160">Non esiste un ruolo per un'istruzione BEGIN TRANSACTION o ROLLBACK TRANSACTION esplicita.</span><span class="sxs-lookup"><span data-stu-id="8de89-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="8de89-161">Se il codice rileva una violazione di una regola business, è possibile che il blocco atomico venga terminato con un'istruzione [THROW](http://msdn.microsoft.com/library/ee677615.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8de89-161">If your code detects a violation of a business rule, it can terminate the atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="8de89-162">CREATE PROCEDURE tipica per le stored procedure compilate in modo nativo</span><span class="sxs-lookup"><span data-stu-id="8de89-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="8de89-163">In genere l'istruzione T-SQL per creare una stored procedure compilata in modo nativo è simile al modello seguente:</span><span class="sxs-lookup"><span data-stu-id="8de89-163">Typically the T-SQL to create a natively compiled stored procedure is similar to the following template:</span></span>

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

* <span data-ttu-id="8de89-164">Per TRANSACTION_ISOLATION_LEVEL, SNAPSHOT è il valore più comune per la stored procedure compilata in modo nativo.</span><span class="sxs-lookup"><span data-stu-id="8de89-164">For the TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is the most common value for the natively compiled stored procedure.</span></span> <span data-ttu-id="8de89-165">Tuttavia, è supportato anche un subset degli altri valori:</span><span class="sxs-lookup"><span data-stu-id="8de89-165">However,  a subset of the other values are also supported:</span></span>
  
  * <span data-ttu-id="8de89-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="8de89-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="8de89-167">SERIALIZABLE</span><span class="sxs-lookup"><span data-stu-id="8de89-167">SERIALIZABLE</span></span>
* <span data-ttu-id="8de89-168">Il valore LANGUAGE deve essere presente nella vista sys.languages.</span><span class="sxs-lookup"><span data-stu-id="8de89-168">The LANGUAGE value must be present in the sys.languages view.</span></span>

### <a name="how-to-migrate-a-stored-procedure"></a><span data-ttu-id="8de89-169">Come eseguire la migrazione di una stored procedure</span><span class="sxs-lookup"><span data-stu-id="8de89-169">How to migrate a stored procedure</span></span>
<span data-ttu-id="8de89-170">Passaggi della migrazione:</span><span class="sxs-lookup"><span data-stu-id="8de89-170">The migration steps are:</span></span>

1. <span data-ttu-id="8de89-171">Ottenere lo script CREATE PROCEDURE per la stored procedure interpretata regolare.</span><span class="sxs-lookup"><span data-stu-id="8de89-171">Obtain the CREATE PROCEDURE script to the regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="8de89-172">Riscrivere l'intestazione in modo che corrisponda al modello precedente.</span><span class="sxs-lookup"><span data-stu-id="8de89-172">Rewrite its header to match the previous template.</span></span>
3. <span data-ttu-id="8de89-173">Verificare se il codice T-SQL della stored procedure usa funzionalità non supportate per le stored procedure compilate in modo nativo.</span><span class="sxs-lookup"><span data-stu-id="8de89-173">Ascertain whether the stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="8de89-174">Se necessario, implementare le soluzioni alternative.</span><span class="sxs-lookup"><span data-stu-id="8de89-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="8de89-175">Per altre informazioni vedere [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="8de89-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="8de89-176">Rinominare la stored procedure precedente tramite SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="8de89-176">Rename the old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="8de89-177">In alternativa usare semplicemente DROP.</span><span class="sxs-lookup"><span data-stu-id="8de89-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="8de89-178">Eseguire lo script CREATE PROCEDURE T-SQL modificato.</span><span class="sxs-lookup"><span data-stu-id="8de89-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="8de89-179">Passaggio 6: Eseguire il carico di lavoro nel test</span><span class="sxs-lookup"><span data-stu-id="8de89-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="8de89-180">Eseguire un carico di lavoro nel database di test simile al carico di lavoro eseguito nel database di produzione.</span><span class="sxs-lookup"><span data-stu-id="8de89-180">Run a workload in your test database that is similar to the workload that runs in your production database.</span></span> <span data-ttu-id="8de89-181">Dovrebbe indicare il miglioramento delle prestazioni ottenuto con l'uso della funzionalità in memoria per tabelle e stored procedure.</span><span class="sxs-lookup"><span data-stu-id="8de89-181">This should reveal the performance gain achieved by your use of the In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="8de89-182">Gli attributi principali del carico di lavoro sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="8de89-182">Major attributes of the workload are:</span></span>

* <span data-ttu-id="8de89-183">Numero di connessioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="8de89-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="8de89-184">Rapporto di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="8de89-184">Read/write ratio.</span></span>

<span data-ttu-id="8de89-185">Per personalizzare ed eseguire il carico di lavoro di test, si consiglia di usare il pratico strumento ostress.exe, illustrato [qui](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="8de89-185">To tailor and run the test workload, consider using the handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="8de89-186">Per ridurre al minimo la latenza di rete, eseguire il test nella stessa area geografica di Azure in cui è disponibile il database.</span><span class="sxs-lookup"><span data-stu-id="8de89-186">To minimize network latency, run your test in the same Azure geographic region where the database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="8de89-187">Passaggio 7: Monitoraggio post-implementazione</span><span class="sxs-lookup"><span data-stu-id="8de89-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="8de89-188">Tenere sotto controllo gli effetti sulle prestazioni delle implementazioni in memoria nell'ambiente di produzione:</span><span class="sxs-lookup"><span data-stu-id="8de89-188">Consider monitoring the performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="8de89-189">[Monitorare l'archiviazione in memoria](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="8de89-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="8de89-190">Monitoraggio del database SQL di Azure tramite le visualizzazioni di gestione dinamica</span><span class="sxs-lookup"><span data-stu-id="8de89-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="8de89-191">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="8de89-191">Related links</span></span>
* [<span data-ttu-id="8de89-192">OLTP in memoria (ottimizzazione in memoria)</span><span class="sxs-lookup"><span data-stu-id="8de89-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="8de89-193">Stored procedure compilate in modo nativo</span><span class="sxs-lookup"><span data-stu-id="8de89-193">Introduction to Natively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="8de89-194">Ottimizzazione guidata per la memoria</span><span class="sxs-lookup"><span data-stu-id="8de89-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

