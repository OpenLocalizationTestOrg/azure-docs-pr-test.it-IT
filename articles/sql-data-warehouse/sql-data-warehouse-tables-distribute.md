---
title: Distribuzione di tabelle in SQL Data Warehouse | Documentazione Microsoft
description: Introduzione alla distribuzione di tabelle in SQL Data Warehouse di Azure.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: d0e12bf821a81826a20b8db84e76c48fa60ad9b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="66022-103">Distribuzione di tabelle in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="66022-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="66022-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="66022-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="66022-105">[Tipi di dati][Data Types]</span><span class="sxs-lookup"><span data-stu-id="66022-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="66022-106">[Distribuzione][Distribute]</span><span class="sxs-lookup"><span data-stu-id="66022-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="66022-107">[Indice][Index]</span><span class="sxs-lookup"><span data-stu-id="66022-107">[Index][Index]</span></span>
> * <span data-ttu-id="66022-108">[Partizione][Partition]</span><span class="sxs-lookup"><span data-stu-id="66022-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="66022-109">[Statistiche][Statistics]</span><span class="sxs-lookup"><span data-stu-id="66022-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="66022-110">[Temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="66022-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="66022-111">SQL Data Warehouse è un sistema di database distribuito a elaborazione parallela massiva.</span><span class="sxs-lookup"><span data-stu-id="66022-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="66022-112">Suddividendo i dati e le funzionalità di elaborazione tra più nodi, SQL Data Warehouse offre grande scalabilità, ben oltre qualsiasi sistema singolo.</span><span class="sxs-lookup"><span data-stu-id="66022-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="66022-113">La distribuzione dei dati all'interno di SQL Data Warehouse è tra i fattori principali che permettono di ottenere prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="66022-113">Deciding how to distribute your data within your SQL Data Warehouse is one of the most important factors to achieving optimal performance.</span></span>   <span data-ttu-id="66022-114">Per ottenere prestazioni ottimali è importante ridurre al minimo lo spostamento dei dati e, per fare ciò, è importante scegliere la giusta strategia di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="66022-114">The key to optimal performance is minimizing data movement and in turn the key to minimizing data movement is selecting the right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="66022-115">Comprendere lo spostamento dei dati</span><span class="sxs-lookup"><span data-stu-id="66022-115">Understanding data movement</span></span>
<span data-ttu-id="66022-116">In un sistema MPP i dati di ogni tabella sono suddivisi in più database sottostanti.</span><span class="sxs-lookup"><span data-stu-id="66022-116">In an MPP system, the data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="66022-117">Le query maggiormente ottimizzate in un sistema MPP possono semplicemente essere passate per l'esecuzione sui singoli database distribuiti, senza alcuna interazione con gli altri database.</span><span class="sxs-lookup"><span data-stu-id="66022-117">The most optimized queries on an MPP system can simply be passed through to execute on the individual distributed databases with no interaction between the other databases.</span></span>  <span data-ttu-id="66022-118">Ad esempio, si supponga di avere un database con dati di vendita che contiene due tabelle, per vendite e clienti.</span><span class="sxs-lookup"><span data-stu-id="66022-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="66022-119">Se si ha una query che deve creare un join tra la tabella delle vendite con quella dei clienti e si dividono entrambe le tabelle per numero di cliente, inserendo ogni cliente in un database distinto, tutte le query che uniscono vendite e clienti possono essere risolte all'interno di ogni database senza scambio di informazioni con gli altri database.</span><span class="sxs-lookup"><span data-stu-id="66022-119">If you have a query that needs to join your sales table to your customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of the other databases.</span></span>  <span data-ttu-id="66022-120">Al contrario, se si dividono i dati di vendita per numero d'ordine e i dati dei clienti per numero di cliente, qualsiasi database specificato non avrà i dati corrispondenti per ogni cliente e quindi se vogliono unire i dati di vendita con quelli dei clienti, sarà necessario ottenere i dati per ogni cliente dagli altri database.</span><span class="sxs-lookup"><span data-stu-id="66022-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have the corresponding data for each customer and thus if you wanted to join your sales data to your customer data, you would need to get the data for each customer from the other databases.</span></span>  <span data-ttu-id="66022-121">Nel secondo esempio lo spostamento dei dati si renderà necessario per spostare i dati dei cliente nei dati di vendita, in modo da consentire l'unione delle due tabelle.</span><span class="sxs-lookup"><span data-stu-id="66022-121">In this second example, data movement would need to occur to move the customer data to the sales data, so that the two tables can be joined.</span></span>  

<span data-ttu-id="66022-122">Lo spostamento dei dati non è sempre una procedura negativa, talvolta è necessaria per risolvere una query.</span><span class="sxs-lookup"><span data-stu-id="66022-122">Data movement isn't always a bad thing, sometimes it's necessary to solve a query.</span></span>  <span data-ttu-id="66022-123">Quando tuttavia è possibile evitare questo passaggio supplementare, la query verrà naturalmente eseguita più velocemente.</span><span class="sxs-lookup"><span data-stu-id="66022-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="66022-124">In genere lo spostamento dei dati si verifica quando le tabelle vengono unite in join o vengono eseguite aggregazioni.</span><span class="sxs-lookup"><span data-stu-id="66022-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="66022-125">Spesso è necessario eseguire entrambe le operazioni, quindi anche se si può procedere all'ottimizzazione per uno scenario, ad esempio un join, lo spostamento dei dati è comunque necessario per facilitare la risoluzione per l'altro scenario, ad esempio un'aggregazione.</span><span class="sxs-lookup"><span data-stu-id="66022-125">Often you need to do both, so while you may be able to optimize for one scenario, like a join, you still need data movement to help you solve for the other scenario, like an aggregation.</span></span>  <span data-ttu-id="66022-126">Il trucco è scoprire quale delle due soluzioni è meno impegnativa.</span><span class="sxs-lookup"><span data-stu-id="66022-126">The trick is figuring out which is less work.</span></span>  <span data-ttu-id="66022-127">Nella maggior parte dei casi, la distribuzione di tabelle dei fatti di grandi dimensioni in una colonna di join comune è il metodo più efficace per ridurre al minimo lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="66022-127">In most cases, distributing large fact tables on a commonly joined column is the most effective method for reducing the most data movement.</span></span>  <span data-ttu-id="66022-128">La distribuzione dei dati nelle colonne di join è un metodo molto più comune per ridurre lo spostamento dei dati rispetto alla distribuzione di dati nelle colonne coinvolte in un'aggregazione.</span><span class="sxs-lookup"><span data-stu-id="66022-128">Distributing data on join columns is a much more common method to reduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="66022-129">Selezionare il metodo di distribuzione</span><span class="sxs-lookup"><span data-stu-id="66022-129">Select distribution method</span></span>
<span data-ttu-id="66022-130">Operando in background, SQL Data Warehouse divide i dati in 60 database.</span><span class="sxs-lookup"><span data-stu-id="66022-130">Behind the scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="66022-131">Un singolo database è detto **distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="66022-131">Each individual database is referred to as a **distribution**.</span></span>  <span data-ttu-id="66022-132">Quando i dati vengono caricati nelle singole tabelle, SQL Data Warehouse deve sapere come dividerli nelle 60 distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="66022-132">When data is loaded into each table, SQL Data Warehouse has to know how to divide your data across these 60 distributions.</span></span>  

<span data-ttu-id="66022-133">Il metodo di distribuzione viene definito a livello di tabella e attualmente sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="66022-133">The distribution method is defined at the table level and currently there are two choices:</span></span>

1. <span data-ttu-id="66022-134">**Round robin** , che distribuisce i dati in modo uniforme ma casuale.</span><span class="sxs-lookup"><span data-stu-id="66022-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="66022-135">**Distribuzione hash** , che distribuisce i dati in base ai valori hash di una singola colonna.</span><span class="sxs-lookup"><span data-stu-id="66022-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="66022-136">Per impostazione predefinita, quando non si definisce un metodo di distribuzione dei dati, per la tabella viene usato il metodo di distribuzione **round robin** .</span><span class="sxs-lookup"><span data-stu-id="66022-136">By default, when you do not define a data distribution method, your table will be distributed using the **round robin** distribution method.</span></span>  <span data-ttu-id="66022-137">Tuttavia, man mano che l'implementazione si fa più sofisticata, è consigliabile usare tabelle con **distribuzione hash** per ridurre al minimo lo spostamento dei dati, ottimizzando così le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="66022-137">However, as you become more sophisticated in your implementation, you will want to consider using **hash distributed** tables to minimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="66022-138">Tabelle round robin</span><span class="sxs-lookup"><span data-stu-id="66022-138">Round Robin Tables</span></span>
<span data-ttu-id="66022-139">Il metodo round robin per la distribuzione dei dati è molto semplice da usare.</span><span class="sxs-lookup"><span data-stu-id="66022-139">Using the Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="66022-140">Man mano che i dati vengono caricati, ogni riga viene semplicemente inviata alla distribuzione successiva.</span><span class="sxs-lookup"><span data-stu-id="66022-140">As your data is loaded, each row is simply sent to the next distribution.</span></span>  <span data-ttu-id="66022-141">Questo metodo distribuisce sempre i dati in modo casuale e molto uniforme in tutte le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="66022-141">This method of distributing the data will always randomly distribute the data very evenly across all of the distributions.</span></span>  <span data-ttu-id="66022-142">In altre parole, durante il processo round robin che inserisce i dati non viene eseguita alcuna operazione di ordinamento.</span><span class="sxs-lookup"><span data-stu-id="66022-142">That is, there is no sorting done during the round robin process which places your data.</span></span>  <span data-ttu-id="66022-143">Per questo motivo, una distribuzione round robin viene a volte definita hash causale.</span><span class="sxs-lookup"><span data-stu-id="66022-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="66022-144">In una tabella con distribuzione round robin non è necessario comprendere i dati.</span><span class="sxs-lookup"><span data-stu-id="66022-144">With a round-robin distributed table there is no need to understand the data.</span></span>  <span data-ttu-id="66022-145">Per questo motivo le tabelle round robin sono spesso un'ottima scelta come destinazioni di caricamento.</span><span class="sxs-lookup"><span data-stu-id="66022-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="66022-146">Per impostazione predefinita, se non viene scelto un metodo di distribuzione, viene usato il metodo di distribuzione round robin.</span><span class="sxs-lookup"><span data-stu-id="66022-146">By default, if no distribution method is chosen, the round robin distribution method will be used.</span></span>  <span data-ttu-id="66022-147">Tuttavia, se è vero che le tabelle round robin sono facili da usare, perché i dati vengono distribuiti in modo casuale nel sistema, è anche vero che il sistema non può garantire la posizione di ogni riga nella distribuzione.</span><span class="sxs-lookup"><span data-stu-id="66022-147">However, while round robin tables are easy to use, because data is randomly distributed across the system it means that the system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="66022-148">Di conseguenza, a volte il sistema deve richiamare un'operazione di spostamento dei dati per organizzare meglio i dati e poter risolvere una query.</span><span class="sxs-lookup"><span data-stu-id="66022-148">As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query.</span></span>  <span data-ttu-id="66022-149">Questo passaggio aggiuntivo può rallentare le query.</span><span class="sxs-lookup"><span data-stu-id="66022-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="66022-150">Si consideri l'uso della distribuzione round robin della tabella negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="66022-150">Consider using Round Robin distribution for your table in the following scenarios:</span></span>

* <span data-ttu-id="66022-151">Quando si inizia come punto di partenza semplice.</span><span class="sxs-lookup"><span data-stu-id="66022-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="66022-152">Se non è presente una chiave di join ovvia.</span><span class="sxs-lookup"><span data-stu-id="66022-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="66022-153">Se non è presente una colonna candidata ottimale per la distribuzione hash della tabella.</span><span class="sxs-lookup"><span data-stu-id="66022-153">If there is not good candidate column for hash distributing the table</span></span>
* <span data-ttu-id="66022-154">Se la tabella non condivide una chiave di join comune con altre tabelle.</span><span class="sxs-lookup"><span data-stu-id="66022-154">If the table does not share a common join key with other tables</span></span>
* <span data-ttu-id="66022-155">Se il join è meno significativo di altri join nella query.</span><span class="sxs-lookup"><span data-stu-id="66022-155">If the join is less significant than other joins in the query</span></span>
* <span data-ttu-id="66022-156">Quando si tratta di una tabella di staging temporaneo.</span><span class="sxs-lookup"><span data-stu-id="66022-156">When the table is a temporary staging table</span></span>

<span data-ttu-id="66022-157">Entrambi gli esempi seguenti creano una tabella round robin:</span><span class="sxs-lookup"><span data-stu-id="66022-157">Both of these examples will create a Round Robin Table:</span></span>

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> <span data-ttu-id="66022-158">Anche se la tabella round robin è il tipo predefinito, la procedura consigliata è essere espliciti nella DDL in modo che le intenzioni del layout di tabella siano chiare.</span><span class="sxs-lookup"><span data-stu-id="66022-158">While round robin is the default table type being explicit in your DDL is considered a best practice so that the intentions of your table layout are clear to others.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="66022-159">Tabelle con distribuzione hash</span><span class="sxs-lookup"><span data-stu-id="66022-159">Hash Distributed Tables</span></span>
<span data-ttu-id="66022-160">L'uso di un algoritmo di **distribuzione hash** per distribuire le tabelle permette di migliorare le prestazioni in molti scenari riducendo lo spostamento dei dati in fase di query.</span><span class="sxs-lookup"><span data-stu-id="66022-160">Using a **Hash distributed** algorithm to distribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="66022-161">Le tabelle con distribuzione hash vengono suddivise tra i database distribuiti usando un algoritmo di hash in una singola colonna selezionata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="66022-161">Hash distributed tables are tables which are divided between the distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="66022-162">La colonna di distribuzione determina il modo in cui i dati vengono divisi tra i database distribuiti.</span><span class="sxs-lookup"><span data-stu-id="66022-162">The distribution column is what determines how the data is divided across your distributed databases.</span></span>  <span data-ttu-id="66022-163">La funzione hash usa la colonna di distribuzione per assegnare righe alle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="66022-163">The hash function uses the distribution column to assign rows to distributions.</span></span>  <span data-ttu-id="66022-164">L'algoritmo di hash e la distribuzione risultante sono deterministici.</span><span class="sxs-lookup"><span data-stu-id="66022-164">The hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="66022-165">Vale a dire che per lo stesso valore con lo stesso tipo di dati viene sempre eseguito l'hash alla stessa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="66022-165">That is the same value with the same data type will always has to the same distribution.</span></span>    

<span data-ttu-id="66022-166">Questo esempio permette di creare una tabella distribuita:</span><span class="sxs-lookup"><span data-stu-id="66022-166">This example will create a table distributed on id:</span></span>

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a><span data-ttu-id="66022-167">Selezionare la colonna di distribuzione</span><span class="sxs-lookup"><span data-stu-id="66022-167">Select distribution column</span></span>
<span data-ttu-id="66022-168">Per eseguire la **distribuzione hash** di una tabella, è necessario selezionare una singola colonna di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="66022-168">When you choose to **hash distribute** a table, you will need to select a single distribution column.</span></span>  <span data-ttu-id="66022-169">Quando si seleziona una colonna di distribuzione occorre prendere in considerazione tre fattori importanti.</span><span class="sxs-lookup"><span data-stu-id="66022-169">When selecting a distribution column, there are three major factors to consider.</span></span>  

<span data-ttu-id="66022-170">Selezionare una singola colonna:</span><span class="sxs-lookup"><span data-stu-id="66022-170">Select a single column which will:</span></span>

1. <span data-ttu-id="66022-171">da non aggiornare,</span><span class="sxs-lookup"><span data-stu-id="66022-171">Not be updated</span></span>
2. <span data-ttu-id="66022-172">per distribuire i dati in modo uniforme, evitando asimmetrie,</span><span class="sxs-lookup"><span data-stu-id="66022-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="66022-173">per ridurre al minimo lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="66022-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="66022-174">Selezionare una colonna di distribuzione da non aggiornare</span><span class="sxs-lookup"><span data-stu-id="66022-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="66022-175">Le colonne di distribuzione non sono aggiornabili. Occorre quindi selezionare una colonna con valori statici.</span><span class="sxs-lookup"><span data-stu-id="66022-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="66022-176">Se una colonna deve essere aggiornata, in generale non è un buon candidato per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="66022-176">If a column will need to be updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="66022-177">Nel caso in cui sia necessario aggiornare una colonna di distribuzione, è possibile procedere prima di tutto eliminando la riga e poi inserendone una nuova.</span><span class="sxs-lookup"><span data-stu-id="66022-177">If there is a case where you must update a distribution column, this can be done by first deleting the row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="66022-178">Selezionare una colonna di distribuzione per distribuire i dati in modo uniforme</span><span class="sxs-lookup"><span data-stu-id="66022-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="66022-179">Dal momento che le prestazioni di un sistema distribuito equivalgono a quelle della distribuzione più lenta, è importante dividere il carico di lavoro in modo uniforme tra le distribuzioni per ottenere un'esecuzione bilanciata in tutto il sistema.</span><span class="sxs-lookup"><span data-stu-id="66022-179">Since a distributed system performs only as fast as its slowest distribution, it is important to divide the work evenly across the distributions in order to achieve balanced execution across the system.</span></span>  <span data-ttu-id="66022-180">Il modo in cui il carico lavoro viene diviso in un sistema distribuito dipende da dove si trovano i dati per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="66022-180">The way the work is divided on a distributed system is based on where the data for each distribution lives.</span></span>  <span data-ttu-id="66022-181">Per questo motivo è molto importante selezionare la colonna di distribuzione appropriata per distribuire i dati, in modo che ogni distribuzione abbia lo stesso carico di lavoro e impieghi lo stesso tempo a completarlo.</span><span class="sxs-lookup"><span data-stu-id="66022-181">This makes it very important to select the right distribution column for distributing the data so that each distribution has equal work and will take the same time to complete its portion of the work.</span></span>  <span data-ttu-id="66022-182">Quando lavoro è diviso equamente nel sistema, i dati vengono bilanciati tra le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="66022-182">When work is well divided across the system, the data is balanced across the distributions.</span></span>  <span data-ttu-id="66022-183">Quando i dati non sono bilanciati in modo uniforme, si parla di **differenze di dati**.</span><span class="sxs-lookup"><span data-stu-id="66022-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="66022-184">Per dividere i dati in modo uniforme ed evitare asimmetrie dei dati, selezionare la colonna di distribuzione tenendo presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="66022-184">To divide data evenly and avoid data skew, consider the following when selecting your distribution column:</span></span>

1. <span data-ttu-id="66022-185">Selezionare una colonna che contiene un numero significativo di valori distinct.</span><span class="sxs-lookup"><span data-stu-id="66022-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="66022-186">Evitare di distribuire dati in colonne con pochi valori distinti.</span><span class="sxs-lookup"><span data-stu-id="66022-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="66022-187">Evitare di distribuire dati in colonne con una frequenza elevata di valori Null.</span><span class="sxs-lookup"><span data-stu-id="66022-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="66022-188">Evitare di distribuire i dati in colonne data.</span><span class="sxs-lookup"><span data-stu-id="66022-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="66022-189">Dato che per ogni valore viene eseguito l'hash in 1 delle 60 distribuzioni, per ottenere una distribuzione uniforme è consigliabile selezionare una colonna altamente univoca che contenga più di 60 valori univoci.</span><span class="sxs-lookup"><span data-stu-id="66022-189">Since each value is hashed to 1 of 60 distributions, to achieve even distribution you will want to select a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="66022-190">Per illustrare questo concetto, si consideri il caso di una colonna contenente solo 40 valori univoci.</span><span class="sxs-lookup"><span data-stu-id="66022-190">To illustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="66022-191">Se la colonna è stata selezionata come chiave di distribuzione, i dati per la tabella potrebbero essere ricevuti su 40 distribuzioni al massimo, lasciando 20 distribuzioni senza dati o elaborazioni da eseguire.</span><span class="sxs-lookup"><span data-stu-id="66022-191">If this column was selected as the distribution key, the data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing to do.</span></span>  <span data-ttu-id="66022-192">Al contrario, le altre 40 distribuzioni avrebbero un carico di lavoro maggiore rispetto a una distribuzione uniforme su 60 distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="66022-192">Conversely, the other 40 distributions would have more work to do that if the data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="66022-193">Questo scenario è un esempio di differenza di dati.</span><span class="sxs-lookup"><span data-stu-id="66022-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="66022-194">Nel sistema MPP, ogni passaggio della query che tutte le distribuzioni completino la loro parte di lavoro.</span><span class="sxs-lookup"><span data-stu-id="66022-194">In MPP system, each query step waits for all distributions to complete their share of the work.</span></span>  <span data-ttu-id="66022-195">Se una distribuzione svolge più lavoro rispetto alle altre, allora le risorse delle altre distribuzioni vengono essenzialmente sprecate nell'attesa della distribuzione occupata.</span><span class="sxs-lookup"><span data-stu-id="66022-195">If one distribution is doing more work than the others, then the resource of the other distributions are essentially wasted just waiting on the busy distribution.</span></span>  <span data-ttu-id="66022-196">Quando si lavoro non viene distribuito uniformemente tra tutte le distribuzioni, si parla di **differenza di elaborazioni**.</span><span class="sxs-lookup"><span data-stu-id="66022-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="66022-197">La differenza di elaborazioni causa un rallentamento delle query rispetto a quando un carico di lavoro può essere distribuito uniformemente in tutte le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="66022-197">Processing skew will cause queries to run slower than if the workload can be evenly spread across the distributions.</span></span>  <span data-ttu-id="66022-198">La differenza di dati porta alla differenza di elaborazioni.</span><span class="sxs-lookup"><span data-stu-id="66022-198">Data skew will lead to processing skew.</span></span>

<span data-ttu-id="66022-199">Evitare di distribuire su una colonna con un elevato numero di valori Null, poiché questi verranno ricevuti nella stessa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="66022-199">Avoid distributing on highly nullable column as the null values will all land on the same distribution.</span></span> <span data-ttu-id="66022-200">Anche la distribuzione in una colonna di data può causare una differenza di elaborazioni, perché tutti i dati per una determinata data verranno ricevuti nella stessa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="66022-200">Distributing on a date column can also cause processing skew because all data for a given date will land on the same distribution.</span></span> <span data-ttu-id="66022-201">Se più utenti eseguono query che applicano tutte un filtro alla stessa data, solo 1 delle 60 distribuzioni svolgerà tutto il lavoro, dal momento che una determinata data sarà solo in una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="66022-201">If several users are executing queries all filtering on the same date, then only 1 of the 60 distributions will be doing all of the work since a given date will only be on one distribution.</span></span> <span data-ttu-id="66022-202">In questo scenario le query verranno probabilmente eseguite 60 volte più lentamente rispetto a quando i dati vengono distribuiti uniformemente in tutte le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="66022-202">In this scenario, the queries will likely run 60 times slower than if the data were equally spread over all of the distributions.</span></span>

<span data-ttu-id="66022-203">Quando non sono disponibili colonne candidate, è consigliabile usare il metodo di distribuzione round robin.</span><span class="sxs-lookup"><span data-stu-id="66022-203">When no good candidate columns exist, then consider using round robin as the distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="66022-204">Selezionare una colonna di distribuzione per ridurre al minimo lo spostamento dei dati</span><span class="sxs-lookup"><span data-stu-id="66022-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="66022-205">Ridurre al minimo lo spostamento dei dati selezionando la colonna di distribuzione appropriata è una delle strategie principali per l'ottimizzazione delle prestazioni di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="66022-205">Minimizing data movement by selecting the right distribution column is one of the most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="66022-206">In genere lo spostamento dei dati si verifica quando le tabelle vengono unite in join o vengono eseguite aggregazioni.</span><span class="sxs-lookup"><span data-stu-id="66022-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="66022-207">Le colonne usate nelle clausole `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` e `HAVING` sono **ottimi** candidati per la distribuzione hash.</span><span class="sxs-lookup"><span data-stu-id="66022-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="66022-208">D'altro canto, le colonne nella clausola `WHERE`**non** sono candidate ottimali come colonne hash, perché limitano le distribuzioni che fanno parte della query, causando una differenza di elaborazioni.</span><span class="sxs-lookup"><span data-stu-id="66022-208">On the other hand, columns in the `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in the query, causing processing skew.</span></span>  <span data-ttu-id="66022-209">Un buon esempio di una colonna che su si potrebbe essere tentati di distribuire, ma che spesso può causare una differenza di elaborazioni è una colonna di data.</span><span class="sxs-lookup"><span data-stu-id="66022-209">A good example of a column which might be tempting to distribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="66022-210">In generale, se sono disponibili due tabelle dei fatti di grandi dimensioni, spesso coinvolte in un join, le prestazioni migliori si otterranno con la distribuzione di entrambe le tabelle in una delle colonne di join.</span><span class="sxs-lookup"><span data-stu-id="66022-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain the most performance by distributing both tables on one of the join columns.</span></span>  <span data-ttu-id="66022-211">Se è presente una tabella che non è mai stata unita a un'altra tabella dei fatti di grandi dimensioni, esaminare le colonne che sono spesso nella clausola `GROUP BY` .</span><span class="sxs-lookup"><span data-stu-id="66022-211">If you have a table that is never joined to another large fact table, then look to columns that are frequently in the `GROUP BY` clause.</span></span>

<span data-ttu-id="66022-212">Esistono alcuni criteri fondamentali che devono essere soddisfatti per evitare lo spostamento dei dati durante un join:</span><span class="sxs-lookup"><span data-stu-id="66022-212">There are a few key criteria which must be met to avoid data movement during a join:</span></span>

1. <span data-ttu-id="66022-213">È necessario eseguire la distribuzione hash delle tabelle coinvolte nel join in **una** delle colonne che fanno parte del join.</span><span class="sxs-lookup"><span data-stu-id="66022-213">The tables involved in the join must be hash distributed on **one** of the columns participating in the join.</span></span>
2. <span data-ttu-id="66022-214">I tipi di dati delle colonne di join nelle due tabelle devono corrispondere.</span><span class="sxs-lookup"><span data-stu-id="66022-214">The data types of the join columns must match between both tables.</span></span>
3. <span data-ttu-id="66022-215">Le colonne devono essere unite con un operatore Uguale.</span><span class="sxs-lookup"><span data-stu-id="66022-215">The columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="66022-216">Il tipo di join può non essere `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="66022-216">The join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="66022-217">Risoluzione dei problemi relativi alle asimmetrie dei dati</span><span class="sxs-lookup"><span data-stu-id="66022-217">Troubleshooting data skew</span></span>
<span data-ttu-id="66022-218">Quando i dati di una tabella sono distribuiti mediante il metodo di distribuzione hash, alcune distribuzioni presenteranno molti più dati di altre.</span><span class="sxs-lookup"><span data-stu-id="66022-218">When table data is distributed using the hash distribution method there is a chance that some distributions will be skewed to have disproportionately more data than others.</span></span> <span data-ttu-id="66022-219">Un'asimmetria dei dati eccessiva può compromettere le prestazioni delle query, perché per il risultato finale di una query distribuita è necessario aspettare che termini la distribuzione con il tempo di esecuzione più lungo.</span><span class="sxs-lookup"><span data-stu-id="66022-219">Excessive data skew can impact query performance because the final result of a distributed query must wait for the longest running distribution to finish.</span></span> <span data-ttu-id="66022-220">A seconda del grado di differenza dati potrebbe essere necessario risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="66022-220">Depending on the degree of the data skew you might need to address it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="66022-221">Identificazione dell'asimmetria dei dati</span><span class="sxs-lookup"><span data-stu-id="66022-221">Identifying skew</span></span>
<span data-ttu-id="66022-222">Un modo semplice per identificare una differenza nelle tabelle consiste nell'uso di `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="66022-222">A simple way to identify a table as skewed is to use `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="66022-223">Questo è un metodo molto semplice e rapido per vedere il numero di righe della tabella archiviate in ognuna delle 60 distribuzioni del database.</span><span class="sxs-lookup"><span data-stu-id="66022-223">This is a very quick and simple way to see the number of table rows that are stored in each of the 60 distributions of your database.</span></span>  <span data-ttu-id="66022-224">Tenere presente che per ottenere prestazioni più bilanciate, le righe nella tabella distribuita vanno suddivise in modo uniforme in tutte le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="66022-224">Remember that for the most balanced performance, the rows in your distributed table should be spread evenly across all the distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="66022-225">Se tuttavia si esegue una query sulle viste a gestione dinamica di Azure SQL Data Warehouse (DMV) è possibile ottenere un'analisi più dettagliata.</span><span class="sxs-lookup"><span data-stu-id="66022-225">However, if you query the Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="66022-226">Per iniziare, creare la vista [dbo.vTableSizes][dbo.vTableSizes] usando il codice SQL fornito nell'articolo [Panoramica delle tabelle][Overview].</span><span class="sxs-lookup"><span data-stu-id="66022-226">To start, create the view [dbo.vTableSizes][dbo.vTableSizes] view using the SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="66022-227">Dopo aver creato la vista, eseguire questa query per identificare le tabelle con un'asimmetria dei dati superiore al 10%.</span><span class="sxs-lookup"><span data-stu-id="66022-227">Once the view is created, run this query to identify which tables have more than 10% data skew.</span></span>

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a><span data-ttu-id="66022-228">Risoluzione delle asimmetrie di distribuzione</span><span class="sxs-lookup"><span data-stu-id="66022-228">Resolving data skew</span></span>
<span data-ttu-id="66022-229">Non tutte le asimmetrie sono sufficienti a giustificare una correzione.</span><span class="sxs-lookup"><span data-stu-id="66022-229">Not all skew is enough to warrant a fix.</span></span>  <span data-ttu-id="66022-230">In alcuni casi, le prestazioni di una tabella in alcune query possono compensare il danno causato dalla distribuzione asimmetrica.</span><span class="sxs-lookup"><span data-stu-id="66022-230">In some cases, the performance of a table in some queries can outweigh the harm of data skew.</span></span>  <span data-ttu-id="66022-231">Per decidere se sia necessario risolvere la differenza dati di una tabella, è necessario conoscere nel modo più completo possibile i volumi di dati e le query del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="66022-231">To decide if you should resolve data skew in a table, you should understand as much as possible about the data volumes and queries in your workload.</span></span>   <span data-ttu-id="66022-232">Per esaminare l'impatto della differenza sulle prestazioni delle query e in particolare sul tempo di completamento delle query nelle singole distribuzioni, è possibile seguire la procedura riportata nell'articolo [Monitoraggio delle query][Query Monitoring].</span><span class="sxs-lookup"><span data-stu-id="66022-232">One way to look at the impact of skew is to use the steps in the [Query Monitoring][Query Monitoring] article to monitor the impact of skew on query performance and specifically the impact to how long queries take to complete on the individual distributions.</span></span>

<span data-ttu-id="66022-233">La distribuzione è essenzialmente l'individuazione del giusto equilibrio fra la minimizzazione della differenza dati e la minimizzazione dello spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="66022-233">Distributing data is a matter of finding the right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="66022-234">Questi obiettivi possono essere contrastanti e talvolta può essere necessario tollerare una determinata differenza dati per poter ridurre lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="66022-234">These can be opposing goals, and sometimes you will want to keep data skew in order to reduce data movement.</span></span> <span data-ttu-id="66022-235">Ad esempio, quando la colonna di distribuzione corrisponde con un'elevata frequenza alla colonna condivisa di join e aggregazioni, si ridurrà al minimo lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="66022-235">For example, when the distribution column is frequently the shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="66022-236">Il vantaggio di uno spostamento dei dati minimo potrebbe essere quello di compensare l'impatto negativo della differenza dati.</span><span class="sxs-lookup"><span data-stu-id="66022-236">The benefit of having the minimal data movement might outweigh the impact of having data skew.</span></span>

<span data-ttu-id="66022-237">Il modo più comune per risolvere la differenza dati è ricreare la tabella con una colonna di distribuzione diversa.</span><span class="sxs-lookup"><span data-stu-id="66022-237">The typical way to resolve data skew is to re-create the table with a different distribution column.</span></span> <span data-ttu-id="66022-238">Dato che non è possibile modificare la colonna di distribuzione in una tabella esistente, per modificare la distribuzione di una tabella occorre crearla nuovamente con [CTAS][].</span><span class="sxs-lookup"><span data-stu-id="66022-238">Since there is no way to change the distribution column on an existing table, the way to change the distribution of a table it to recreate it with a [CTAS][].</span></span>  <span data-ttu-id="66022-239">Di seguito sono riportati due esempi di risoluzione di distribuzioni asimmetriche dei dati:</span><span class="sxs-lookup"><span data-stu-id="66022-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-the-table-with-a-new-distribution-column"></a><span data-ttu-id="66022-240">Esempio 1: Ricreare la tabella con una nuova colonna di distribuzione</span><span class="sxs-lookup"><span data-stu-id="66022-240">Example 1: Re-create the table with a new distribution column</span></span>
<span data-ttu-id="66022-241">Questo esempio usa [CTAS][] per ricreare una tabella con una colonna di distribuzione hash diversa.</span><span class="sxs-lookup"><span data-stu-id="66022-241">This example uses [CTAS][] to re-create a table with a different hash distribution column.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] TO [FactInternetSales];
```

### <a name="example-2-re-create-the-table-using-round-robin-distribution"></a><span data-ttu-id="66022-242">Esempio 2: Ricreare la tabella usando la distribuzione round robin</span><span class="sxs-lookup"><span data-stu-id="66022-242">Example 2: Re-create the table using round robin distribution</span></span>
<span data-ttu-id="66022-243">Questo esempio usa [CTAS][] per ricreare una tabella con una distribuzione round robin anziché una distribuzione hash.</span><span class="sxs-lookup"><span data-stu-id="66022-243">This example uses [CTAS][] to re-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="66022-244">Questa modifica produce una distribuzione uniforme dei dati ma aumenta lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="66022-244">This change will produce even data distribution at the cost of increased data movement.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] TO [FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="66022-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="66022-245">Next steps</span></span>
<span data-ttu-id="66022-246">Per altre informazioni sulla progettazione di tabelle, vedere gli articoli relativi a [distribuzione][Distribute], [indici][Index], [partizioni][Partition], [tipi di dati][Data Types], [statistiche][Statistics] e [tabelle temporanee][Temporary].</span><span class="sxs-lookup"><span data-stu-id="66022-246">To learn more about table design, see the [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="66022-247">Per una panoramica delle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="66022-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
