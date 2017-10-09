---
title: aaaMigrate il tooSQL dello schema del Data Warehouse | Documenti Microsoft
description: Suggerimenti per la migrazione del tooAzure schema SQL Data Warehouse per lo sviluppo di soluzioni.
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
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a><span data-ttu-id="787cd-103">Eseguire la migrazione del Data Warehouse di tooSQL schemi</span><span class="sxs-lookup"><span data-stu-id="787cd-103">Migrate your schemas tooSQL Data Warehouse</span></span>
<span data-ttu-id="787cd-104">Indicazioni per la migrazione del tooSQL gli schemi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="787cd-104">Guidance for migrating your SQL schemas tooSQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="787cd-105">Pianificare la migrazione dello schema</span><span class="sxs-lookup"><span data-stu-id="787cd-105">Plan your schema migration</span></span>

<span data-ttu-id="787cd-106">Quando si pianifica una migrazione, vedere hello [Cenni preliminari su tabella] [ table overview] toobecome familiarità con le considerazioni sulla progettazione di tabella, ad esempio le statistiche, distribuzione, il partizionamento e l'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="787cd-106">As you plan a migration, see hello [table overview][table overview] toobecome familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="787cd-107">Vengono anche presentate alcune [funzionalità non supportate per le tabelle][unsupported table features] e le soluzioni alternative.</span><span class="sxs-lookup"><span data-stu-id="787cd-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a><span data-ttu-id="787cd-108">Utilizzare i database tooconsolidate degli schemi definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="787cd-108">Use user-defined schemas tooconsolidate databases</span></span>

<span data-ttu-id="787cd-109">È probabile che carico di lavoro esistente includa più di un database.</span><span class="sxs-lookup"><span data-stu-id="787cd-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="787cd-110">Ad esempio un data warehouse di SQL Server può includere un database di staging, un database del data warehouse e alcuni database del data mart.</span><span class="sxs-lookup"><span data-stu-id="787cd-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="787cd-111">In questa topologia ogni database viene eseguito come carico di lavoro separato con criteri di protezione separati.</span><span class="sxs-lookup"><span data-stu-id="787cd-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="787cd-112">Al contrario, SQL Data Warehouse viene eseguito hello intero data warehouse del carico di lavoro all'interno di un database.</span><span class="sxs-lookup"><span data-stu-id="787cd-112">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="787cd-113">I join tra database non sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="787cd-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="787cd-114">Pertanto, Data Warehouse di SQL prevede che tutte le tabelle utilizzate da hello dati warehouse toobe archiviati all'interno di un database di hello.</span><span class="sxs-lookup"><span data-stu-id="787cd-114">Therefore, SQL Data Warehouse expects all tables used by hello data warehouse toobe stored within hello one database.</span></span>

<span data-ttu-id="787cd-115">È consigliabile utilizzare gli schemi definiti dall'utente tooconsolidate il carico di lavoro esistente in un database.</span><span class="sxs-lookup"><span data-stu-id="787cd-115">We recommend using user-defined schemas tooconsolidate your existing workload into one database.</span></span> <span data-ttu-id="787cd-116">Per esempi, vedere [Schemi definiti dall'utente](sql-data-warehouse-develop-user-defined-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="787cd-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="787cd-117">Usare tipi di dati compatibili</span><span class="sxs-lookup"><span data-stu-id="787cd-117">Use compatible data types</span></span>
<span data-ttu-id="787cd-118">Modificare il toobe di tipi di dati compatibile con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="787cd-118">Modify your data types toobe compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="787cd-119">Per l'elenco dei tipi di dati supportati e non supportati, vedere [Tipi di dati][data types].</span><span class="sxs-lookup"><span data-stu-id="787cd-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="787cd-120">Questo argomento offre soluzioni alternative per i tipi di hello non supportato.</span><span class="sxs-lookup"><span data-stu-id="787cd-120">That topic gives workarounds for hello unsupported types.</span></span> <span data-ttu-id="787cd-121">Fornisce inoltre una query tooidentify i tipi esistenti che non sono supportati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="787cd-121">It also provides a query tooidentify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="787cd-122">Ridurre al minimo le dimensioni delle righe</span><span class="sxs-lookup"><span data-stu-id="787cd-122">Minimize row size</span></span>
<span data-ttu-id="787cd-123">Per prestazioni ottimali, ridurre al minimo la lunghezza di riga hello delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="787cd-123">For best performance, minimize hello row length of your tables.</span></span> <span data-ttu-id="787cd-124">Poiché le lunghezze riga più brevi comportare prestazioni toobetter, utilizzare i tipi di dati più piccolo hello che funzionano per i dati.</span><span class="sxs-lookup"><span data-stu-id="787cd-124">Since shorter row lengths lead toobetter performance, use hello smallest data types that work for your data.</span></span> 

<span data-ttu-id="787cd-125">Per la larghezza della riga della tabella, PolyBase ha un limite pari a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="787cd-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="787cd-126">Se si prevede dati tooload in SQL Data Warehouse con PolyBase, aggiornare le larghezze di riga massimo tabelle toohave di minore di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="787cd-126">If you plan tooload data into SQL Data Warehouse with PolyBase, update your tables toohave maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a><span data-ttu-id="787cd-127">Specificare l'opzione di distribuzione hello</span><span class="sxs-lookup"><span data-stu-id="787cd-127">Specify hello distribution option</span></span>
<span data-ttu-id="787cd-128">SQL Data Warehouse è un sistema di database distribuito.</span><span class="sxs-lookup"><span data-stu-id="787cd-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="787cd-129">Ogni tabella è distribuita o replicato in nodi di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="787cd-129">Each table is distributed or replicated across hello Compute nodes.</span></span> <span data-ttu-id="787cd-130">È disponibile un'opzione di tabella che consente di specificare la modalità toodistribute hello dati.</span><span class="sxs-lookup"><span data-stu-id="787cd-130">There's a table option that lets you specify how toodistribute hello data.</span></span> <span data-ttu-id="787cd-131">scelte di Hello sono round-robin, replicate, o hash distribuito.</span><span class="sxs-lookup"><span data-stu-id="787cd-131">hello choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="787cd-132">Ognuna presenta vantaggi e svantaggi.</span><span class="sxs-lookup"><span data-stu-id="787cd-132">Each has pros and cons.</span></span> <span data-ttu-id="787cd-133">Se non si specifica l'opzione di distribuzione hello, SQL Data Warehouse userà round robin come predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="787cd-133">If you don't specify hello distribution option, SQL Data Warehouse will use round-robin as hello default.</span></span>

- <span data-ttu-id="787cd-134">Round-robin è predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="787cd-134">Round-robin is hello default.</span></span> <span data-ttu-id="787cd-135">È più semplice toouse di hello e carica i dati di hello più rapidamente possibile, ma join richiede lo spostamento dei dati che determina un rallentamento delle prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="787cd-135">It is hello simplest toouse, and loads hello data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="787cd-136">Replicati archivia una copia della tabella hello in ogni nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="787cd-136">Replicated stores a copy of hello table on each Compute node.</span></span> <span data-ttu-id="787cd-137">Le tabelle replicate sono efficienti perché non richiedono lo spostamento di dati per i join e le aggregazioni.</span><span class="sxs-lookup"><span data-stu-id="787cd-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="787cd-138">Tuttavia richiedono risorse di archiviazione aggiuntive e di conseguenza sono la scelta migliore per tabelle di dimensioni contenute.</span><span class="sxs-lookup"><span data-stu-id="787cd-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="787cd-139">Hash distribuita distribuisce le righe di hello in tutti i nodi di hello tramite una funzione hash.</span><span class="sxs-lookup"><span data-stu-id="787cd-139">Hash distributed distributes hello rows across all hello nodes via a hash function.</span></span> <span data-ttu-id="787cd-140">Poiché sono progettate tooprovide prestazioni elevate delle query in tabelle di grandi dimensioni, tabelle hash distribuiti sono cuore hello del Data Warehouse di SQL.</span><span class="sxs-lookup"><span data-stu-id="787cd-140">Hash distributed tables are hello heart of SQL Data Warehouse since they are designed tooprovide high query performance on large tables.</span></span> <span data-ttu-id="787cd-141">Questa opzione richiede alcune pianificazione tooselect hello migliore colonna sulla quale toodistribute hello.</span><span class="sxs-lookup"><span data-stu-id="787cd-141">This option requires some planning tooselect hello best column on which toodistribute hello data.</span></span> <span data-ttu-id="787cd-142">Tuttavia, se non si sceglie hello colonna migliore hello prima volta, è possibile nuovamente distribuire facilmente hello dati in una colonna diversa.</span><span class="sxs-lookup"><span data-stu-id="787cd-142">However, if you don't choose hello best column hello first time, you can easily re-distribute hello data on a different column.</span></span> 

<span data-ttu-id="787cd-143">toochoose hello migliore opzione di distribuzione per ogni tabella, vedere [Distributed tabelle](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="787cd-143">toochoose hello best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="787cd-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="787cd-144">Next steps</span></span>
<span data-ttu-id="787cd-145">Dopo avere eseguito la migrazione tooSQL di schema del database del Data Warehouse, procedere tooone di hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="787cd-145">Once you have successfully migrated your database schema tooSQL Data Warehouse, proceed tooone of hello following articles:</span></span>

* <span data-ttu-id="787cd-146">[Eseguire la migrazione dei dati][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="787cd-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="787cd-147">[Eseguire la migrazione del codice][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="787cd-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="787cd-148">Per ulteriori informazioni sulle procedure consigliate di SQL Data Warehouse, vedere hello [consigliate] [ best practices] articolo.</span><span class="sxs-lookup"><span data-stu-id="787cd-148">For more about SQL Data Warehouse best practices, see hello [best practices][best practices] article.</span></span>

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
