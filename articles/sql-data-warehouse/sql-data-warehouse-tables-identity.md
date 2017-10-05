---
title: Creare chiavi surrogate con IDENTITY | Microsoft Docs
description: Informazioni su come usare IDENTITY per creare chiavi surrogate per le tabelle.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 3ab5d159e6eaeb830135fe134e108b0e4de4b7d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="26445-103">Creare chiavi surrogate con IDENTITY</span><span class="sxs-lookup"><span data-stu-id="26445-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="26445-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="26445-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="26445-105">[Tipi di dati][Data Types]</span><span class="sxs-lookup"><span data-stu-id="26445-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="26445-106">[Distribuzione][Distribute]</span><span class="sxs-lookup"><span data-stu-id="26445-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="26445-107">[Indice][Index]</span><span class="sxs-lookup"><span data-stu-id="26445-107">[Index][Index]</span></span>
> * <span data-ttu-id="26445-108">[Partizione][Partition]</span><span class="sxs-lookup"><span data-stu-id="26445-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="26445-109">[Statistiche][Statistics]</span><span class="sxs-lookup"><span data-stu-id="26445-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="26445-110">[Temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="26445-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="26445-111">[Identità][Identity]</span><span class="sxs-lookup"><span data-stu-id="26445-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="26445-112">Molti progettisti di modelli di dati preferiscono creare chiavi surrogate sulle tabelle durante la progettazione dei modelli per i data warehouse.</span><span class="sxs-lookup"><span data-stu-id="26445-112">Many data modelers like to create surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="26445-113">È possibile usare la proprietà IDENTITY per raggiungere questo obiettivo in modo semplice ed efficace senza effetti sulle prestazioni di caricamento.</span><span class="sxs-lookup"><span data-stu-id="26445-113">You can use the IDENTITY property to achieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="26445-114">Introduzione a IDENTITY</span><span class="sxs-lookup"><span data-stu-id="26445-114">Get started with IDENTITY</span></span>
<span data-ttu-id="26445-115">È possibile definire una tabella con la proprietà IDENTITY al momento della creazione, usando una sintassi simile all'istruzione seguente:</span><span class="sxs-lookup"><span data-stu-id="26445-115">You can define a table as having the IDENTITY property when you first create the table by using syntax that is similar to the following statement:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

<span data-ttu-id="26445-116">È quindi possibile usare `INSERT..SELECT` per popolare la tabella.</span><span class="sxs-lookup"><span data-stu-id="26445-116">You can then use `INSERT..SELECT` to populate the table.</span></span>

## <a name="behavior"></a><span data-ttu-id="26445-117">Comportamento</span><span class="sxs-lookup"><span data-stu-id="26445-117">Behavior</span></span>
<span data-ttu-id="26445-118">La proprietà IDENTITY è progettata per supportare la scalabilità orizzontale tra tutte le distribuzioni nel data warehouse senza influenzare le prestazioni di caricamento.</span><span class="sxs-lookup"><span data-stu-id="26445-118">The IDENTITY property is designed to scale out across all the distributions in the data warehouse without affecting load performance.</span></span> <span data-ttu-id="26445-119">Pertanto, l'implementazione di IDENTITY è orientata al raggiungimento di questi obiettivi.</span><span class="sxs-lookup"><span data-stu-id="26445-119">Therefore, the implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="26445-120">Questa sezione illustra le varie sfumature dell'implementazione per comprenderle appieno.</span><span class="sxs-lookup"><span data-stu-id="26445-120">This section highlights the nuances of the implementation to help you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="26445-121">Allocazione dei valori</span><span class="sxs-lookup"><span data-stu-id="26445-121">Allocation of values</span></span>
<span data-ttu-id="26445-122">La proprietà IDENTITY non garantisce l'ordine di allocazione dei valori surrogati, in modo conforme al comportamento di SQL Server e del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="26445-122">The IDENTITY property doesn't guarantee the order in which the surrogate values are allocated, which reflects the behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="26445-123">Tuttavia, in Azure SQL Data Warehouse, l'assenza di una garanzia è più evidente.</span><span class="sxs-lookup"><span data-stu-id="26445-123">However, in Azure SQL Data Warehouse, the absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="26445-124">L'esempio seguente è una dimostrazione:</span><span class="sxs-lookup"><span data-stu-id="26445-124">The following example is an illustration:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

<span data-ttu-id="26445-125">Nell'esempio precedente due righe raggiungono la distribuzione 1.</span><span class="sxs-lookup"><span data-stu-id="26445-125">In the preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="26445-126">La prima riga ha il valore surrogato 1 nella colonna `C1` e la seconda riga ha il valore surrogato 61.</span><span class="sxs-lookup"><span data-stu-id="26445-126">The first row has the surrogate value of 1 in column `C1`, and the second row has the surrogate value of 61.</span></span> <span data-ttu-id="26445-127">Entrambi questi valori sono stati generati dalla proprietà IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="26445-127">Both of these values were generated by the IDENTITY property.</span></span> <span data-ttu-id="26445-128">L'allocazione dei valori non è tuttavia contigua.</span><span class="sxs-lookup"><span data-stu-id="26445-128">However, the allocation of the values is not contiguous.</span></span> <span data-ttu-id="26445-129">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="26445-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="26445-130">Dati asimmetrici</span><span class="sxs-lookup"><span data-stu-id="26445-130">Skewed data</span></span> 
<span data-ttu-id="26445-131">L'intervallo di valori per il tipo di dati è distribuito uniformemente tra le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="26445-131">The range of values for the data type are spread evenly across the distributions.</span></span> <span data-ttu-id="26445-132">Nel caso di una tabella distribuita con dati asimmetrici, l'intervallo di valori disponibili per il tipo di dati può esaurirsi in modo anomalo.</span><span class="sxs-lookup"><span data-stu-id="26445-132">If a distributed table suffers from skewed data, then the range of values available to the datatype can be exhausted prematurely.</span></span> <span data-ttu-id="26445-133">Ad esempio, se tutti i dati vengono destinati a una singola distribuzione, la tabella ha effettivamente accesso solo a un sessantesimo dei valori del tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="26445-133">For example, if all the data ends up in a single distribution, then effectively the table has access to only one-sixtieth of the values of the data type.</span></span> <span data-ttu-id="26445-134">Per questo motivo, la proprietà IDENTITY è limitata solo ai tipi di dati `INT` e `BIGINT`.</span><span class="sxs-lookup"><span data-stu-id="26445-134">For this reason, the IDENTITY property is limited to `INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="26445-135">SELECT..INTO</span><span class="sxs-lookup"><span data-stu-id="26445-135">SELECT..INTO</span></span>
<span data-ttu-id="26445-136">Quando una colonna IDENTITY esistente viene selezionata in una nuova tabella, la nuova colonna eredita la proprietà IDENTITY, a meno che non sia vera una delle condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="26445-136">When an existing IDENTITY column is selected into a new table, the new column inherits the IDENTITY property, unless one of the following conditions is true:</span></span>
- <span data-ttu-id="26445-137">L'istruzione SELECT contiene un join.</span><span class="sxs-lookup"><span data-stu-id="26445-137">The SELECT statement contains a join.</span></span>
- <span data-ttu-id="26445-138">Più istruzioni SELECT sono unite in join tramite l'istruzione UNION.</span><span class="sxs-lookup"><span data-stu-id="26445-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="26445-139">La colonna IDENTITY è elencata più di una volta nell'elenco SELECT.</span><span class="sxs-lookup"><span data-stu-id="26445-139">The IDENTITY column is listed more than one time in the SELECT list.</span></span>
- <span data-ttu-id="26445-140">La colonna IDENTITY fa parte di un'espressione.</span><span class="sxs-lookup"><span data-stu-id="26445-140">The IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="26445-141">Se una di queste condizioni è vera, la colonna viene creata come NOT NULL invece di ereditare la proprietà IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="26445-141">If any one of these conditions is true, the column is created NOT NULL instead of inheriting the IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="26445-142">CREATE TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="26445-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="26445-143">CREATE TABLE AS SELECT (CTAS) ha lo stesso comportamento di SQL Server documentato per SELECT... INTO.</span><span class="sxs-lookup"><span data-stu-id="26445-143">CREATE TABLE AS SELECT (CTAS) follows the same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="26445-144">Tuttavia, non è possibile specificare una proprietà IDENTITY nella definizione di colonna della parte `CREATE TABLE` dell'istruzione.</span><span class="sxs-lookup"><span data-stu-id="26445-144">However, you can't specify an IDENTITY property in the column definition of the `CREATE TABLE` part of the statement.</span></span> <span data-ttu-id="26445-145">Non è possibile nemmeno usare la funzione IDENTITY nella parte `SELECT` dell'istruzione CTAS.</span><span class="sxs-lookup"><span data-stu-id="26445-145">You also can't use the IDENTITY function in the `SELECT` part of the CTAS.</span></span> <span data-ttu-id="26445-146">Per popolare una tabella, è necessario usare l'istruzione `CREATE TABLE` per definire la tabella, seguita da `INSERT..SELECT` per popolarla.</span><span class="sxs-lookup"><span data-stu-id="26445-146">To populate a table, you need to use `CREATE TABLE` to define the table followed by `INSERT..SELECT` to populate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="26445-147">Inserire in modo esplicito valori in una colonna IDENTITY</span><span class="sxs-lookup"><span data-stu-id="26445-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="26445-148">SQL Data Warehouse supporta la sintassi `SET IDENTITY_INSERT <your table> ON|OFF`.</span><span class="sxs-lookup"><span data-stu-id="26445-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="26445-149">È possibile usare questa sintassi per inserire in modo esplicito i valori nella colonna IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="26445-149">You can use this syntax to explicitly insert values into the IDENTITY column.</span></span>

<span data-ttu-id="26445-150">Molti progettisti di modelli di dati preferiscono usare valori negativi predefiniti per alcune righe nelle dimensioni.</span><span class="sxs-lookup"><span data-stu-id="26445-150">Many data modelers like to use predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="26445-151">Un esempio è la riga -1 o "membro sconosciuto".</span><span class="sxs-lookup"><span data-stu-id="26445-151">An example is the -1 or "unknown member" row.</span></span> 

<span data-ttu-id="26445-152">Il prossimo script mostra come aggiungere in modo esplicito questa riga tramite SET IDENTITY_INSERT:</span><span class="sxs-lookup"><span data-stu-id="26445-152">The next script shows how to explicitly add this row by using SET IDENTITY_INSERT:</span></span>

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="26445-153">Caricare i dati in una tabella con IDENTITY</span><span class="sxs-lookup"><span data-stu-id="26445-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="26445-154">La presenza della proprietà IDENTITY ha alcune implicazioni per il codice di caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="26445-154">The presence of the IDENTITY property has some implications to your data-loading code.</span></span> <span data-ttu-id="26445-155">Questa sezione evidenzia alcuni modelli di base per il caricamento di dati nelle tabelle usando IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="26445-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="26445-156">Caricare dati con PolyBase</span><span class="sxs-lookup"><span data-stu-id="26445-156">Load data with PolyBase</span></span>
<span data-ttu-id="26445-157">Per caricare dati in una tabella e generare una chiave surrogata con IDENTITY, creare la tabella e quindi usare INSERT... SELECT o INSERT... VALUES per eseguire il caricamento.</span><span class="sxs-lookup"><span data-stu-id="26445-157">To load data into a table and generate a surrogate key by using IDENTITY, create the table and then use INSERT..SELECT or INSERT..VALUES to perform the load.</span></span>

<span data-ttu-id="26445-158">L'esempio seguente illustra il modello di base:</span><span class="sxs-lookup"><span data-stu-id="26445-158">The following example highlights the basic pattern:</span></span>
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT to populate the table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> <span data-ttu-id="26445-159">Non è attualmente possibile usare `CREATE TABLE AS SELECT` per il caricamento di dati in una tabella con una colonna IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="26445-159">It's not possible to use `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="26445-160">Per altre informazioni sul caricamento dei dati tramite lo strumento BCP (Bulk Copy Program), vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="26445-160">For more information on loading data by using the bulk copy program (BCP) tool, see the following articles:</span></span>

- <span data-ttu-id="26445-161">[Caricare dati con PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="26445-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="26445-162">[Procedure consigliate per PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="26445-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="26445-163">Caricare dati con BCP</span><span class="sxs-lookup"><span data-stu-id="26445-163">Load data with BCP</span></span>
<span data-ttu-id="26445-164">BCP è uno strumento da riga di comando utilizzabile per caricare dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="26445-164">BCP is a command-line tool that you can use to load data into SQL Data Warehouse.</span></span> <span data-ttu-id="26445-165">Uno dei parametri di questo strumento (-E) controlla il comportamento di BCP quando si caricano dati in una tabella con una colonna IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="26445-165">One of its parameters (-E) controls the behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="26445-166">Quando viene specificato il parametro -E, vengono mantenuti i valori contenuti nel file di input per la colonna con IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="26445-166">When -E is specified, the values held in the input file for the column with IDENTITY are retained.</span></span> <span data-ttu-id="26445-167">Se -E *non* viene specificato, i valori in questa colonna vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="26445-167">If -E is *not* specified, then the values in this column are ignored.</span></span> <span data-ttu-id="26445-168">Se la colonna IDENTITY non è inclusa, i dati vengono caricati come di consueto.</span><span class="sxs-lookup"><span data-stu-id="26445-168">If the identity column is not included, then the data is loaded as normal.</span></span> <span data-ttu-id="26445-169">I valori vengono generati in base al criterio di incremento e seeding della proprietà.</span><span class="sxs-lookup"><span data-stu-id="26445-169">The values are generated according to the increment and seed policy of the property.</span></span>

<span data-ttu-id="26445-170">Per altre informazioni sul caricamento di dati con BCP, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="26445-170">For more information on loading data by using BCP, see the following articles:</span></span>

- <span data-ttu-id="26445-171">[Caricare dati con BCP][]</span><span class="sxs-lookup"><span data-stu-id="26445-171">[Load with BCP][]</span></span>
- <span data-ttu-id="26445-172">[BCP in MSDN][]</span><span class="sxs-lookup"><span data-stu-id="26445-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="26445-173">Viste del catalogo</span><span class="sxs-lookup"><span data-stu-id="26445-173">Catalog views</span></span>
<span data-ttu-id="26445-174">SQL Data Warehouse supporta la vista del catalogo `sys.identity_columns`.</span><span class="sxs-lookup"><span data-stu-id="26445-174">SQL Data Warehouse supports the `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="26445-175">Questa vista è utilizzabile per identificare una colonna con la proprietà IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="26445-175">This view can be used to identify a column that has the IDENTITY property.</span></span>

<span data-ttu-id="26445-176">Per comprendere meglio lo schema del database, questo esempio mostra come integrare `sys.identity_columns` con altre viste del catalogo di sistema:</span><span class="sxs-lookup"><span data-stu-id="26445-176">To help you better understand the database schema, this example shows how to integrate `sys.identity_columns` with other system catalog views:</span></span>

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a><span data-ttu-id="26445-177">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="26445-177">Limitations</span></span>
<span data-ttu-id="26445-178">La proprietà IDENTITY non può essere usata negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="26445-178">The IDENTITY property can't be used in the following scenarios:</span></span>
- <span data-ttu-id="26445-179">Quando il tipo di dati della colonna non è INT o BIGINT</span><span class="sxs-lookup"><span data-stu-id="26445-179">Where the column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="26445-180">Quando la colonna è anche la chiave di distribuzione</span><span class="sxs-lookup"><span data-stu-id="26445-180">Where the column is also the distribution key</span></span>
- <span data-ttu-id="26445-181">Quando la tabella è una tabella esterna</span><span class="sxs-lookup"><span data-stu-id="26445-181">Where the table is an external table</span></span> 

<span data-ttu-id="26445-182">Le funzioni correlate seguenti non sono supportate in SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="26445-182">The following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="26445-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="26445-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="26445-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="26445-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="26445-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="26445-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="26445-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="26445-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="26445-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="26445-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="26445-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="26445-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="26445-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="26445-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="26445-190">Attività</span><span class="sxs-lookup"><span data-stu-id="26445-190">Tasks</span></span>

<span data-ttu-id="26445-191">Questa sezione include esempi di codice utilizzabili per eseguire attività comuni quando si usano colonne IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="26445-191">This section provides some sample code you can use to perform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="26445-192">La colonna C1 è la colonna IDENTITY in tutte le attività seguenti.</span><span class="sxs-lookup"><span data-stu-id="26445-192">Column C1 is the IDENTITY in all the following tasks.</span></span>
> 
 
### <a name="find-the-highest-allocated-value-for-a-table"></a><span data-ttu-id="26445-193">Individuare il valore massimo allocato per una tabella</span><span class="sxs-lookup"><span data-stu-id="26445-193">Find the highest allocated value for a table</span></span>
<span data-ttu-id="26445-194">Usare la funzione `MAX()` per determinare il valore massimo allocato per una tabella distribuita:</span><span class="sxs-lookup"><span data-stu-id="26445-194">Use the `MAX()` function to determine the highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-the-seed-and-increment-for-the-identity-property"></a><span data-ttu-id="26445-195">Trovare il valore di seeding e incremento per la proprietà IDENTITY</span><span class="sxs-lookup"><span data-stu-id="26445-195">Find the seed and increment for the IDENTITY property</span></span>
<span data-ttu-id="26445-196">È possibile usare le viste del catalogo per individuare i valori di configurazione di incremento e seeding di IDENTITY per una tabella usando la query seguente:</span><span class="sxs-lookup"><span data-stu-id="26445-196">You can use the catalog views to discover the identity increment and seed configuration values for a table by using the following query:</span></span> 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a><span data-ttu-id="26445-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="26445-197">Next steps</span></span>

* <span data-ttu-id="26445-198">Per altre informazioni sullo sviluppo di tabelle, vedere [Panoramica delle tabelle][Overview], [Tipi di dati per le tabelle][Data Types], [Distribuire una tabella][Distribute], [Indicizzare una tabella][Index], [Partizionare una tabella][Partition] e [Tabelle temporanee][Temporary].</span><span class="sxs-lookup"><span data-stu-id="26445-198">To learn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="26445-199">Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="26445-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<span data-ttu-id="26445-200">[Caricare dati con BCP]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span><span class="sxs-lookup"><span data-stu-id="26445-200">[Load with bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span></span>
<span data-ttu-id="26445-201">[Caricare dati con PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span><span class="sxs-lookup"><span data-stu-id="26445-201">[Load with PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span></span>
<span data-ttu-id="26445-202">[Procedure consigliate per PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span><span class="sxs-lookup"><span data-stu-id="26445-202">[PolyBase best practices]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span></span>


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
<span data-ttu-id="26445-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span><span class="sxs-lookup"><span data-stu-id="26445-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span></span>
<span data-ttu-id="26445-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span><span class="sxs-lookup"><span data-stu-id="26445-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span></span>
<span data-ttu-id="26445-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span><span class="sxs-lookup"><span data-stu-id="26445-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span></span>
<span data-ttu-id="26445-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span><span class="sxs-lookup"><span data-stu-id="26445-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span></span>
<span data-ttu-id="26445-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span><span class="sxs-lookup"><span data-stu-id="26445-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span></span>
<span data-ttu-id="26445-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span><span class="sxs-lookup"><span data-stu-id="26445-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span></span>
<span data-ttu-id="26445-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span><span class="sxs-lookup"><span data-stu-id="26445-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span></span>

<span data-ttu-id="26445-210">[bcp in MSDN]: https://msdn.microsoft.com/library/ms162802.aspx</span><span class="sxs-lookup"><span data-stu-id="26445-210">[bcp in MSDN]: https://msdn.microsoft.com/library/ms162802.aspx</span></span>
  

<!--Other Web references-->  
