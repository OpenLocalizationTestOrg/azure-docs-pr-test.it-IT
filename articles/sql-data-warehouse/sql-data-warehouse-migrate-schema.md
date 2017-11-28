---
title: Eseguire la migrazione dello schema in SQL Data Warehouse | Documentazione Microsoft
description: Suggerimenti per la migrazione dello schema in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 07ca2321852e276502187e768177e7e82bdfd080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-schemas-to-sql-data-warehouse"></a><span data-ttu-id="4ae3f-103">Eseguire la migrazione degli schemi a SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4ae3f-103">Migrate your schemas to SQL Data Warehouse</span></span>
<span data-ttu-id="4ae3f-104">Indicazioni per la migrazione degli schemi SQL a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-104">Guidance for migrating your SQL schemas to SQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="4ae3f-105">Pianificare la migrazione dello schema</span><span class="sxs-lookup"><span data-stu-id="4ae3f-105">Plan your schema migration</span></span>

<span data-ttu-id="4ae3f-106">Per pianificare una migrazione vedere la [panoramica delle tabelle][table overview] per aspetti della creazione delle tabelle come statistiche, distribuzione, partizionamento e indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-106">As you plan a migration, see the [table overview][table overview] to become familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="4ae3f-107">Vengono anche presentate alcune [funzionalità non supportate per le tabelle][unsupported table features] e le soluzioni alternative.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-to-consolidate-databases"></a><span data-ttu-id="4ae3f-108">Usare gli schemi definiti dall'utente per consolidare i database</span><span class="sxs-lookup"><span data-stu-id="4ae3f-108">Use user-defined schemas to consolidate databases</span></span>

<span data-ttu-id="4ae3f-109">È probabile che carico di lavoro esistente includa più di un database.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="4ae3f-110">Ad esempio un data warehouse di SQL Server può includere un database di staging, un database del data warehouse e alcuni database del data mart.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="4ae3f-111">In questa topologia ogni database viene eseguito come carico di lavoro separato con criteri di protezione separati.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="4ae3f-112">Al contrario, SQL Data Warehouse esegue tutto il carico di lavoro del data warehouse all'interno di un database.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-112">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="4ae3f-113">I join tra database non sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="4ae3f-114">SQL Data Warehouse prevede pertanto che tutte le tabelle usate dal data warehouse siano archiviate in un unico database.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-114">Therefore, SQL Data Warehouse expects all tables used by the data warehouse to be stored within the one database.</span></span>

<span data-ttu-id="4ae3f-115">È consigliabile usare schemi definiti dall'utente per consolidare il carico di lavoro esistente in un unico database.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-115">We recommend using user-defined schemas to consolidate your existing workload into one database.</span></span> <span data-ttu-id="4ae3f-116">Per esempi, vedere [Schemi definiti dall'utente](sql-data-warehouse-develop-user-defined-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="4ae3f-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="4ae3f-117">Usare tipi di dati compatibili</span><span class="sxs-lookup"><span data-stu-id="4ae3f-117">Use compatible data types</span></span>
<span data-ttu-id="4ae3f-118">Modificare i tipi di dati in modo che siano compatibili con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-118">Modify your data types to be compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="4ae3f-119">Per l'elenco dei tipi di dati supportati e non supportati, vedere [Tipi di dati][data types].</span><span class="sxs-lookup"><span data-stu-id="4ae3f-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="4ae3f-120">L'argomento offre soluzioni alternative per i tipi non supportati.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-120">That topic gives workarounds for the unsupported types.</span></span> <span data-ttu-id="4ae3f-121">Offre anche una query per identificare i tipi esistenti che non sono supportati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-121">It also provides a query to identify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="4ae3f-122">Ridurre al minimo le dimensioni delle righe</span><span class="sxs-lookup"><span data-stu-id="4ae3f-122">Minimize row size</span></span>
<span data-ttu-id="4ae3f-123">Per prestazioni ottimali, ridurre al minimo la lunghezza delle righe delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-123">For best performance, minimize the row length of your tables.</span></span> <span data-ttu-id="4ae3f-124">Dato che a righe più brevi corrispondono prestazioni migliori, usare i tipi di dati più brevi che funzionano per i dati.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-124">Since shorter row lengths lead to better performance, use the smallest data types that work for your data.</span></span> 

<span data-ttu-id="4ae3f-125">Per la larghezza della riga della tabella, PolyBase ha un limite pari a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="4ae3f-126">Se si prevede di caricare dati in SQL Data Warehouse con PolyBase, aggiornare le tabelle in modo che le righe abbiano una larghezza massima inferiore a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-126">If you plan to load data into SQL Data Warehouse with PolyBase, update your tables to have maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but the largest possible size of the row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and the defined row width is less than one MB. When loading rows, PolyBase allocates the full length of the variable-length data. The full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-the-distribution-option"></a><span data-ttu-id="4ae3f-127">Specificare l'opzione di distribuzione</span><span class="sxs-lookup"><span data-stu-id="4ae3f-127">Specify the distribution option</span></span>
<span data-ttu-id="4ae3f-128">SQL Data Warehouse è un sistema di database distribuito.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="4ae3f-129">Ogni tabella è distribuita o replicata nei nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-129">Each table is distributed or replicated across the Compute nodes.</span></span> <span data-ttu-id="4ae3f-130">Un'opzione della tabella consente di specificare la modalità di distribuzione dei dati.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-130">There's a table option that lets you specify how to distribute the data.</span></span> <span data-ttu-id="4ae3f-131">Le scelte disponibili sono round robin, replica o distribuzione hash.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-131">The choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="4ae3f-132">Ognuna presenta vantaggi e svantaggi.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-132">Each has pros and cons.</span></span> <span data-ttu-id="4ae3f-133">Se non si specifica l'opzione di distribuzione, SQL Data Warehouse usa round robin come impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-133">If you don't specify the distribution option, SQL Data Warehouse will use round-robin as the default.</span></span>

- <span data-ttu-id="4ae3f-134">La modalità round robin è la modalità predefinita.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-134">Round-robin is the default.</span></span> <span data-ttu-id="4ae3f-135">È la più semplice da usare e carica i dati alla massima velocità, ma lo spostamento di dati richiesto dai join determina un rallentamento delle prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-135">It is the simplest to use, and loads the data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="4ae3f-136">Nell'approccio con tabelle replicate, viene archiviata una copia della tabella in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-136">Replicated stores a copy of the table on each Compute node.</span></span> <span data-ttu-id="4ae3f-137">Le tabelle replicate sono efficienti perché non richiedono lo spostamento di dati per i join e le aggregazioni.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="4ae3f-138">Tuttavia richiedono risorse di archiviazione aggiuntive e di conseguenza sono la scelta migliore per tabelle di dimensioni contenute.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="4ae3f-139">La distribuzione hash distribuisce le righe su tutti i nodi tramite una funzione hash.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-139">Hash distributed distributes the rows across all the nodes via a hash function.</span></span> <span data-ttu-id="4ae3f-140">Le tabelle con distribuzione hash sono il nucleo di SQL Data Warehouse e sono progettate per garantire alte prestazioni per le query su tabelle di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-140">Hash distributed tables are the heart of SQL Data Warehouse since they are designed to provide high query performance on large tables.</span></span> <span data-ttu-id="4ae3f-141">Questa opzione richiede un certo grado di pianificazione nella scelta della colonna ottimale per la distribuzione dei dati.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-141">This option requires some planning to select the best column on which to distribute the data.</span></span> <span data-ttu-id="4ae3f-142">Se tuttavia al primo tentativo non si sceglie la colonna migliore, è possibile ridistribuire facilmente i dati in base a un'altra colonna.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-142">However, if you don't choose the best column the first time, you can easily re-distribute the data on a different column.</span></span> 

<span data-ttu-id="4ae3f-143">Per scegliere la migliore opzione di distribuzione per ogni tabella, vedere [Tabelle con distribuzione](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="4ae3f-143">To choose the best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="4ae3f-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ae3f-144">Next steps</span></span>
<span data-ttu-id="4ae3f-145">Dopo la migrazione dello schema del database a SQL Data Warehouse, passare a uno degli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ae3f-145">Once you have successfully migrated your database schema to SQL Data Warehouse, proceed to one of the following articles:</span></span>

* <span data-ttu-id="4ae3f-146">[Eseguire la migrazione dei dati][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="4ae3f-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="4ae3f-147">[Eseguire la migrazione del codice][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="4ae3f-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="4ae3f-148">Per altre informazioni, vedere l'articolo con le [procedure consigliate][best practices] di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4ae3f-148">For more about SQL Data Warehouse best practices, see the [best practices][best practices] article.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
