---
title: "chiavi surrogate aaaCreate utilizzando identità | Documenti Microsoft"
description: "Informazioni su come surrogato toocreate di identità toouse chiavi per le tabelle."
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
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="902fc-103">Creare chiavi surrogate con IDENTITY</span><span class="sxs-lookup"><span data-stu-id="902fc-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="902fc-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="902fc-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="902fc-105">[Tipi di dati][Data Types]</span><span class="sxs-lookup"><span data-stu-id="902fc-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="902fc-106">[Distribuzione][Distribute]</span><span class="sxs-lookup"><span data-stu-id="902fc-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="902fc-107">[Indice][Index]</span><span class="sxs-lookup"><span data-stu-id="902fc-107">[Index][Index]</span></span>
> * <span data-ttu-id="902fc-108">[Partizione][Partition]</span><span class="sxs-lookup"><span data-stu-id="902fc-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="902fc-109">[Statistiche][Statistics]</span><span class="sxs-lookup"><span data-stu-id="902fc-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="902fc-110">[Temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="902fc-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="902fc-111">[Identità][Identity]</span><span class="sxs-lookup"><span data-stu-id="902fc-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="902fc-112">Quando si progettano i modelli di data warehouse, molti progettisti di dati come chiavi surrogate toocreate le tabelle.</span><span class="sxs-lookup"><span data-stu-id="902fc-112">Many data modelers like toocreate surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="902fc-113">È possibile utilizzare hello identità proprietà tooachieve questo obiettivo semplice ed efficace senza influenzare le prestazioni del carico.</span><span class="sxs-lookup"><span data-stu-id="902fc-113">You can use hello IDENTITY property tooachieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="902fc-114">Introduzione a IDENTITY</span><span class="sxs-lookup"><span data-stu-id="902fc-114">Get started with IDENTITY</span></span>
<span data-ttu-id="902fc-115">È possibile definire una tabella con proprietà IDENTITY hello quando si crea la tabella hello utilizzando la sintassi simile toohello istruzione:</span><span class="sxs-lookup"><span data-stu-id="902fc-115">You can define a table as having hello IDENTITY property when you first create hello table by using syntax that is similar toohello following statement:</span></span>

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

<span data-ttu-id="902fc-116">È quindi possibile utilizzare `INSERT..SELECT` tabella hello toopopulate.</span><span class="sxs-lookup"><span data-stu-id="902fc-116">You can then use `INSERT..SELECT` toopopulate hello table.</span></span>

## <a name="behavior"></a><span data-ttu-id="902fc-117">Comportamento</span><span class="sxs-lookup"><span data-stu-id="902fc-117">Behavior</span></span>
<span data-ttu-id="902fc-118">Hello proprietà IDENTITY è progettato tooscale out tra tutte le distribuzioni di hello nel data warehouse di hello senza influenzare le prestazioni del carico.</span><span class="sxs-lookup"><span data-stu-id="902fc-118">hello IDENTITY property is designed tooscale out across all hello distributions in hello data warehouse without affecting load performance.</span></span> <span data-ttu-id="902fc-119">Pertanto, l'implementazione hello dell'identità è orientato per raggiungere questi obiettivi.</span><span class="sxs-lookup"><span data-stu-id="902fc-119">Therefore, hello implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="902fc-120">In questa sezione evidenzia sfumature hello di hello implementazione toohelp comprenderne meglio.</span><span class="sxs-lookup"><span data-stu-id="902fc-120">This section highlights hello nuances of hello implementation toohelp you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="902fc-121">Allocazione dei valori</span><span class="sxs-lookup"><span data-stu-id="902fc-121">Allocation of values</span></span>
<span data-ttu-id="902fc-122">Hello proprietà IDENTITY non garantisce l'ordine di hello in cui hello vengono allocati valori surrogati, che riflette il comportamento di hello di SQL Server e Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="902fc-122">hello IDENTITY property doesn't guarantee hello order in which hello surrogate values are allocated, which reflects hello behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="902fc-123">Tuttavia, in Azure SQL Data Warehouse, mancanza di hello di una garanzia è più evidente.</span><span class="sxs-lookup"><span data-stu-id="902fc-123">However, in Azure SQL Data Warehouse, hello absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="902fc-124">Hello di esempio seguente viene illustrato questo concetto:</span><span class="sxs-lookup"><span data-stu-id="902fc-124">hello following example is an illustration:</span></span>

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

<span data-ttu-id="902fc-125">In hello sopra riportato, due righe ottenuto nella distribuzione 1.</span><span class="sxs-lookup"><span data-stu-id="902fc-125">In hello preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="902fc-126">prima riga Hello ha hello surrogato valore 1 nella colonna `C1`, e hello seconda riga ha valore surrogato hello 61.</span><span class="sxs-lookup"><span data-stu-id="902fc-126">hello first row has hello surrogate value of 1 in column `C1`, and hello second row has hello surrogate value of 61.</span></span> <span data-ttu-id="902fc-127">Entrambi questi valori sono stati generati da hello proprietà IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="902fc-127">Both of these values were generated by hello IDENTITY property.</span></span> <span data-ttu-id="902fc-128">Allocazione di hello dei valori hello, tuttavia, non è contiguo.</span><span class="sxs-lookup"><span data-stu-id="902fc-128">However, hello allocation of hello values is not contiguous.</span></span> <span data-ttu-id="902fc-129">Questo comportamento dipende dalla progettazione.</span><span class="sxs-lookup"><span data-stu-id="902fc-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="902fc-130">Dati asimmetrici</span><span class="sxs-lookup"><span data-stu-id="902fc-130">Skewed data</span></span> 
<span data-ttu-id="902fc-131">Hello intervallo di valori per il tipo di dati hello sono distribuiti uniformemente tra le distribuzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-131">hello range of values for hello data type are spread evenly across hello distributions.</span></span> <span data-ttu-id="902fc-132">In caso di una tabella distribuita da dati asimmetrici, hello quindi l'intervallo di valori può esaurirsi toohello disponibile il tipo di dati in modo anomalo.</span><span class="sxs-lookup"><span data-stu-id="902fc-132">If a distributed table suffers from skewed data, then hello range of values available toohello datatype can be exhausted prematurely.</span></span> <span data-ttu-id="902fc-133">Ad esempio, se tutti i dati di hello finisce in una singola distribuzione, quindi in modo efficace hello tabella ha accesso tooonly sessantesimo a uno dei valori hello hello del tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="902fc-133">For example, if all hello data ends up in a single distribution, then effectively hello table has access tooonly one-sixtieth of hello values of hello data type.</span></span> <span data-ttu-id="902fc-134">Per questo motivo, la proprietà IDENTITY hello è limitato troppo`INT` e `BIGINT` solo i tipi di dati.</span><span class="sxs-lookup"><span data-stu-id="902fc-134">For this reason, hello IDENTITY property is limited too`INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="902fc-135">SELECT..INTO</span><span class="sxs-lookup"><span data-stu-id="902fc-135">SELECT..INTO</span></span>
<span data-ttu-id="902fc-136">Quando una colonna IDENTITY esistente è selezionata in una nuova tabella, hello nuova colonna eredita la proprietà IDENTITY hello, a meno che non viene soddisfatta una delle seguenti condizioni hello:</span><span class="sxs-lookup"><span data-stu-id="902fc-136">When an existing IDENTITY column is selected into a new table, hello new column inherits hello IDENTITY property, unless one of hello following conditions is true:</span></span>
- <span data-ttu-id="902fc-137">istruzione SELECT Hello contiene un join.</span><span class="sxs-lookup"><span data-stu-id="902fc-137">hello SELECT statement contains a join.</span></span>
- <span data-ttu-id="902fc-138">Più istruzioni SELECT sono unite in join tramite l'istruzione UNION.</span><span class="sxs-lookup"><span data-stu-id="902fc-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="902fc-139">colonna IDENTITY Hello è elencata più di una volta nell'elenco di selezione hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-139">hello IDENTITY column is listed more than one time in hello SELECT list.</span></span>
- <span data-ttu-id="902fc-140">colonna IDENTITY Hello fa parte di un'espressione.</span><span class="sxs-lookup"><span data-stu-id="902fc-140">hello IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="902fc-141">Se una di queste condizioni è true, la colonna hello viene creata non NULL, anziché ereditare proprietà IDENTITY hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-141">If any one of these conditions is true, hello column is created NOT NULL instead of inheriting hello IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="902fc-142">CREATE TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="902fc-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="902fc-143">Crea tabella AS selezionare (un'istruzione CTAS) segue hello stesso comportamento SQL Server che è documentato per SELECT... IN.</span><span class="sxs-lookup"><span data-stu-id="902fc-143">CREATE TABLE AS SELECT (CTAS) follows hello same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="902fc-144">Tuttavia, è possibile specificare una proprietà IDENTITY in una definizione di colonna hello di hello `CREATE TABLE` fa parte dell'istruzione hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-144">However, you can't specify an IDENTITY property in hello column definition of hello `CREATE TABLE` part of hello statement.</span></span> <span data-ttu-id="902fc-145">È inoltre possibile utilizzare la funzione di identità hello in hello `SELECT` fa parte di un'istruzione CTAS hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-145">You also can't use hello IDENTITY function in hello `SELECT` part of hello CTAS.</span></span> <span data-ttu-id="902fc-146">toopopulate una tabella, è necessario toouse `CREATE TABLE` toodefine hello tabella seguite dalle `INSERT..SELECT` toopopulate è.</span><span class="sxs-lookup"><span data-stu-id="902fc-146">toopopulate a table, you need toouse `CREATE TABLE` toodefine hello table followed by `INSERT..SELECT` toopopulate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="902fc-147">Inserire in modo esplicito valori in una colonna IDENTITY</span><span class="sxs-lookup"><span data-stu-id="902fc-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="902fc-148">SQL Data Warehouse supporta la sintassi `SET IDENTITY_INSERT <your table> ON|OFF`.</span><span class="sxs-lookup"><span data-stu-id="902fc-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="902fc-149">È possibile utilizzare i valori di insert tooexplicitly questa sintassi nella colonna IDENTITY hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-149">You can use this syntax tooexplicitly insert values into hello IDENTITY column.</span></span>

<span data-ttu-id="902fc-150">Molti progettisti di dati come negativo predefiniti toouse i valori per alcune righe relative dimensioni.</span><span class="sxs-lookup"><span data-stu-id="902fc-150">Many data modelers like toouse predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="902fc-151">Un esempio è hello -1 o la riga "membro sconosciuto".</span><span class="sxs-lookup"><span data-stu-id="902fc-151">An example is hello -1 or "unknown member" row.</span></span> 

<span data-ttu-id="902fc-152">passare allo script successivo Hello viene illustrato come tooexplicitly aggiungere questa riga tramite SET IDENTITY_INSERT:</span><span class="sxs-lookup"><span data-stu-id="902fc-152">hello next script shows how tooexplicitly add this row by using SET IDENTITY_INSERT:</span></span>

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

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="902fc-153">Caricare i dati in una tabella con IDENTITY</span><span class="sxs-lookup"><span data-stu-id="902fc-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="902fc-154">presenza di Hello di hello proprietà IDENTITY include codice implicazioni tooyour il caricamento di dati.</span><span class="sxs-lookup"><span data-stu-id="902fc-154">hello presence of hello IDENTITY property has some implications tooyour data-loading code.</span></span> <span data-ttu-id="902fc-155">Questa sezione evidenzia alcuni modelli di base per il caricamento di dati nelle tabelle usando IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="902fc-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="902fc-156">Caricare dati con PolyBase</span><span class="sxs-lookup"><span data-stu-id="902fc-156">Load data with PolyBase</span></span>
<span data-ttu-id="902fc-157">dati tooload in una tabella e generare una chiave surrogata utilizzando l'identità, creare la tabella hello e quindi utilizza l'istruzione INSERT... SELECT o INSERT... I valori tooperform hello carico.</span><span class="sxs-lookup"><span data-stu-id="902fc-157">tooload data into a table and generate a surrogate key by using IDENTITY, create hello table and then use INSERT..SELECT or INSERT..VALUES tooperform hello load.</span></span>

<span data-ttu-id="902fc-158">Hello esempio seguente vengono evidenziate modello di base hello:</span><span class="sxs-lookup"><span data-stu-id="902fc-158">hello following example highlights hello basic pattern:</span></span>
 
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

--Use INSERT..SELECT toopopulate hello table from an external table
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
> <span data-ttu-id="902fc-159">Non è possibile toouse `CREATE TABLE AS SELECT` attualmente durante il caricamento di dati in una tabella con una colonna IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="902fc-159">It's not possible toouse `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="902fc-160">Per ulteriori informazioni sul caricamento dei dati tramite lo strumento programma (BCP) di copia bulk di hello, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="902fc-160">For more information on loading data by using hello bulk copy program (BCP) tool, see hello following articles:</span></span>

- <span data-ttu-id="902fc-161">[Caricare dati con PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="902fc-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="902fc-162">[Procedure consigliate per PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="902fc-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="902fc-163">Caricare dati con BCP</span><span class="sxs-lookup"><span data-stu-id="902fc-163">Load data with BCP</span></span>
<span data-ttu-id="902fc-164">BCP è uno strumento da riga di comando che è possibile utilizzare dati tooload in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="902fc-164">BCP is a command-line tool that you can use tooload data into SQL Data Warehouse.</span></span> <span data-ttu-id="902fc-165">Uno dei relativi parametri (-E) controlli hello comportamento dell'utilità BCP quando si caricano dati in una tabella con una colonna IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="902fc-165">One of its parameters (-E) controls hello behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="902fc-166">Quando viene specificato -E, vengono mantenuti i valori hello contenuti nel file di input per la colonna hello hello con identità.</span><span class="sxs-lookup"><span data-stu-id="902fc-166">When -E is specified, hello values held in hello input file for hello column with IDENTITY are retained.</span></span> <span data-ttu-id="902fc-167">Se -E è *non* specificato, i valori hello in questa colonna vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="902fc-167">If -E is *not* specified, then hello values in this column are ignored.</span></span> <span data-ttu-id="902fc-168">Se la colonna identity hello non è inclusa, dati hello viene caricati come di consueto.</span><span class="sxs-lookup"><span data-stu-id="902fc-168">If hello identity column is not included, then hello data is loaded as normal.</span></span> <span data-ttu-id="902fc-169">i valori Hello vengono generati in base a criteri toohello di incremento e valore di inizializzazione della proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-169">hello values are generated according toohello increment and seed policy of hello property.</span></span>

<span data-ttu-id="902fc-170">Per ulteriori informazioni sul caricamento dei dati tramite BCP in, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="902fc-170">For more information on loading data by using BCP, see hello following articles:</span></span>

- <span data-ttu-id="902fc-171">[Caricare dati con BCP][]</span><span class="sxs-lookup"><span data-stu-id="902fc-171">[Load with BCP][]</span></span>
- <span data-ttu-id="902fc-172">[BCP in MSDN][]</span><span class="sxs-lookup"><span data-stu-id="902fc-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="902fc-173">Viste del catalogo</span><span class="sxs-lookup"><span data-stu-id="902fc-173">Catalog views</span></span>
<span data-ttu-id="902fc-174">SQL Data Warehouse supporta hello `sys.identity_columns` vista del catalogo.</span><span class="sxs-lookup"><span data-stu-id="902fc-174">SQL Data Warehouse supports hello `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="902fc-175">Questa vista può essere utilizzato tooidentify una colonna che contiene la proprietà IDENTITY hello.</span><span class="sxs-lookup"><span data-stu-id="902fc-175">This view can be used tooidentify a column that has hello IDENTITY property.</span></span>

<span data-ttu-id="902fc-176">toohelp è comprendere meglio lo schema del database hello, questo esempio viene illustrato come toointegrate `sys.identity_columns` con altre viste del catalogo di sistema:</span><span class="sxs-lookup"><span data-stu-id="902fc-176">toohelp you better understand hello database schema, this example shows how toointegrate `sys.identity_columns` with other system catalog views:</span></span>

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

## <a name="limitations"></a><span data-ttu-id="902fc-177">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="902fc-177">Limitations</span></span>
<span data-ttu-id="902fc-178">Hello proprietà IDENTITY non può essere utilizzato in hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="902fc-178">hello IDENTITY property can't be used in hello following scenarios:</span></span>
- <span data-ttu-id="902fc-179">In cui hello colonna non è di tipo INT o BIGINT</span><span class="sxs-lookup"><span data-stu-id="902fc-179">Where hello column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="902fc-180">In cui la colonna hello è anche la chiave di distribuzione hello</span><span class="sxs-lookup"><span data-stu-id="902fc-180">Where hello column is also hello distribution key</span></span>
- <span data-ttu-id="902fc-181">In cui la tabella hello è una tabella esterna</span><span class="sxs-lookup"><span data-stu-id="902fc-181">Where hello table is an external table</span></span> 

<span data-ttu-id="902fc-182">Hello seguenti funzioni correlate non è supportata in SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="902fc-182">hello following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="902fc-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="902fc-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="902fc-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="902fc-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="902fc-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="902fc-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="902fc-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="902fc-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="902fc-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="902fc-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="902fc-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="902fc-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="902fc-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="902fc-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="902fc-190">Attività</span><span class="sxs-lookup"><span data-stu-id="902fc-190">Tasks</span></span>

<span data-ttu-id="902fc-191">In questa sezione fornisce alcuni esempi di codice è possibile utilizzare le attività comuni tooperform quando si lavora con le colonne IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="902fc-191">This section provides some sample code you can use tooperform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="902fc-192">Colonna C1 è hello identità in hello tutte le seguenti attività.</span><span class="sxs-lookup"><span data-stu-id="902fc-192">Column C1 is hello IDENTITY in all hello following tasks.</span></span>
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a><span data-ttu-id="902fc-193">Trovare il valore di hello massima allocata per una tabella</span><span class="sxs-lookup"><span data-stu-id="902fc-193">Find hello highest allocated value for a table</span></span>
<span data-ttu-id="902fc-194">Hello utilizzare `MAX()` funzione toodetermine hello valore massima allocata per una tabella distribuita:</span><span class="sxs-lookup"><span data-stu-id="902fc-194">Use hello `MAX()` function toodetermine hello highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a><span data-ttu-id="902fc-195">Trovare hello inizializzazione e incremento per la proprietà IDENTITY hello</span><span class="sxs-lookup"><span data-stu-id="902fc-195">Find hello seed and increment for hello IDENTITY property</span></span>
<span data-ttu-id="902fc-196">È possibile utilizzare hello catalogo viste toodiscover hello identità di incremento e valore di inizializzazione valori di configurazione per una tabella utilizzando hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="902fc-196">You can use hello catalog views toodiscover hello identity increment and seed configuration values for a table by using hello following query:</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="902fc-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="902fc-197">Next steps</span></span>

* <span data-ttu-id="902fc-198">toolearn più sullo sviluppo di tabelle, vedere [Cenni preliminari su tabella][Overview], [tipi di dati di tabella][Data Types], [distribuireunatabella] [ Distribute], [Indicizzare una tabella][Index], [una tabella di partizione][Partition], e [ Tabelle temporanee][Temporary].</span><span class="sxs-lookup"><span data-stu-id="902fc-198">toolearn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="902fc-199">Per altre informazioni sulle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="902fc-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

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

[Caricare dati con BCP]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Caricare dati con PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[Procedure consigliate per PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[bcp in MSDN]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
