---
title: aaaDistributing nelle tabelle SQL Data Warehouse | Documenti Microsoft
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
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="3ab1a-103">Distribuzione di tabelle in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3ab1a-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="3ab1a-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="3ab1a-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="3ab1a-105">[Tipi di dati][Data Types]</span><span class="sxs-lookup"><span data-stu-id="3ab1a-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="3ab1a-106">[Distribuzione][Distribute]</span><span class="sxs-lookup"><span data-stu-id="3ab1a-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="3ab1a-107">[Indice][Index]</span><span class="sxs-lookup"><span data-stu-id="3ab1a-107">[Index][Index]</span></span>
> * <span data-ttu-id="3ab1a-108">[Partizione][Partition]</span><span class="sxs-lookup"><span data-stu-id="3ab1a-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="3ab1a-109">[Statistiche][Statistics]</span><span class="sxs-lookup"><span data-stu-id="3ab1a-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="3ab1a-110">[Temporanee][Temporary]</span><span class="sxs-lookup"><span data-stu-id="3ab1a-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="3ab1a-111">SQL Data Warehouse è un sistema di database distribuito a elaborazione parallela massiva.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="3ab1a-112">Suddividendo i dati e le funzionalità di elaborazione tra più nodi, SQL Data Warehouse offre grande scalabilità, ben oltre qualsiasi sistema singolo.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="3ab1a-113">Decidere come toodistribute i dati all'interno del Data Warehouse di SQL sono uno dei più importante hello fattori tooachieving ottenere prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-113">Deciding how toodistribute your data within your SQL Data Warehouse is one of hello most important factors tooachieving optimal performance.</span></span>   <span data-ttu-id="3ab1a-114">prestazioni di chiave toooptimal Hello sono ridurre al minimo lo spostamento dei dati e a sua volta lo spostamento dei dati di chiave toominimizing hello seleziona la strategia di distribuzione corretto hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-114">hello key toooptimal performance is minimizing data movement and in turn hello key toominimizing data movement is selecting hello right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="3ab1a-115">Comprendere lo spostamento dei dati</span><span class="sxs-lookup"><span data-stu-id="3ab1a-115">Understanding data movement</span></span>
<span data-ttu-id="3ab1a-116">In un sistema MPP, dati hello da ogni tabella sono suddiviso tra diversi database sottostanti.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-116">In an MPP system, hello data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="3ab1a-117">query Hello più ottimizzata su un sistema MPP possono semplicemente essere trasmessi tramite tooexecute hello singoli database distribuiti senza l'intervento dell'hello tra gli altri database.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-117">hello most optimized queries on an MPP system can simply be passed through tooexecute on hello individual distributed databases with no interaction between hello other databases.</span></span>  <span data-ttu-id="3ab1a-118">Ad esempio, si supponga di avere un database con dati di vendita che contiene due tabelle, per vendite e clienti.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="3ab1a-119">Se si dispone di una query che deve toojoin la tabella di clienti tooyour tabella sales e si divide sia le tabelle e sulle vendite clienti backup per il numero di clienti, l'inserimento di ogni cliente in un database separato, tutte le query che uniscono vendite e clienti possano essere risolti all'interno di ogni database con alcuna conoscenza di hello altri database.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-119">If you have a query that needs toojoin your sales table tooyour customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of hello other databases.</span></span>  <span data-ttu-id="3ab1a-120">Al contrario, se i dati di vendita diviso per il numero di ordine e i dati cliente numero cliente, quindi uno specifico database senza dati corrispondenti hello per ogni cliente e pertanto se si desidera toojoin i dati sui clienti tooyour i dati di vendita, è necessario tooget hello dati per ogni cliente dalla hello altri database.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have hello corresponding data for each customer and thus if you wanted toojoin your sales data tooyour customer data, you would need tooget hello data for each customer from hello other databases.</span></span>  <span data-ttu-id="3ab1a-121">Nel secondo esempio, lo spostamento di dati necessario toooccur toomove hello cliente dati toohello dati di vendita, in modo che hello due tabelle possono essere unite in join.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-121">In this second example, data movement would need toooccur toomove hello customer data toohello sales data, so that hello two tables can be joined.</span></span>  

<span data-ttu-id="3ab1a-122">Lo spostamento dei dati non è sempre un aspetto negativo, in alcuni casi è necessario toosolve una query.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-122">Data movement isn't always a bad thing, sometimes it's necessary toosolve a query.</span></span>  <span data-ttu-id="3ab1a-123">Quando tuttavia è possibile evitare questo passaggio supplementare, la query verrà naturalmente eseguita più velocemente.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="3ab1a-124">In genere lo spostamento dei dati si verifica quando le tabelle vengono unite in join o vengono eseguite aggregazioni.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="3ab1a-125">Spesso è necessario toodo entrambi, in modo mentre è in grado di toooptimize per uno scenario, ad esempio un join, è comunque necessario toohelp lo spostamento dei dati per risolvere per hello altro scenario, ad esempio un'aggregazione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-125">Often you need toodo both, so while you may be able toooptimize for one scenario, like a join, you still need data movement toohelp you solve for hello other scenario, like an aggregation.</span></span>  <span data-ttu-id="3ab1a-126">stratagemma Hello è scoprire che è minore di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-126">hello trick is figuring out which is less work.</span></span>  <span data-ttu-id="3ab1a-127">Nella maggior parte dei casi, la distribuzione delle tabelle dei fatti di grandi dimensioni in una colonna normalmente unite in join è hello metodo più efficace per ridurre hello la maggior parte dello spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-127">In most cases, distributing large fact tables on a commonly joined column is hello most effective method for reducing hello most data movement.</span></span>  <span data-ttu-id="3ab1a-128">Distribuzione dei dati nelle colonne join è un molto più comune di metodo tooreduce lo spostamento dei dati rispetto alla distribuzione di dati nelle colonne coinvolte in un'aggregazione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-128">Distributing data on join columns is a much more common method tooreduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="3ab1a-129">Selezionare il metodo di distribuzione</span><span class="sxs-lookup"><span data-stu-id="3ab1a-129">Select distribution method</span></span>
<span data-ttu-id="3ab1a-130">Dietro le quinte hello SQL Data Warehouse divide i dati in 60 database.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-130">Behind hello scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="3ab1a-131">Ogni singolo database è tooas di cui si fa riferimento un **distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-131">Each individual database is referred tooas a **distribution**.</span></span>  <span data-ttu-id="3ab1a-132">Quando i dati vengono caricati in ogni tabella, SQL Data Warehouse ha tooknow come toodivide i dati in queste 60 distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-132">When data is loaded into each table, SQL Data Warehouse has tooknow how toodivide your data across these 60 distributions.</span></span>  

<span data-ttu-id="3ab1a-133">metodo di distribuzione Hello è definito a livello di tabella hello e attualmente sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="3ab1a-133">hello distribution method is defined at hello table level and currently there are two choices:</span></span>

1. <span data-ttu-id="3ab1a-134">**Round robin** , che distribuisce i dati in modo uniforme ma casuale.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="3ab1a-135">**Distribuzione hash** , che distribuisce i dati in base ai valori hash di una singola colonna.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="3ab1a-136">Per impostazione predefinita, quando si definisce un metodo di distribuzione di dati, la tabella verrà distribuita tramite hello **round robin** metodo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-136">By default, when you do not define a data distribution method, your table will be distributed using hello **round robin** distribution method.</span></span>  <span data-ttu-id="3ab1a-137">Tuttavia, dopo aver acquisito più sofisticati nell'implementazione, è tooconsider utilizzando **hash distribuita** tabelle toominimize lo spostamento dei dati che a sua volta consente di ottimizzare le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-137">However, as you become more sophisticated in your implementation, you will want tooconsider using **hash distributed** tables toominimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="3ab1a-138">Tabelle round robin</span><span class="sxs-lookup"><span data-stu-id="3ab1a-138">Round Robin Tables</span></span>
<span data-ttu-id="3ab1a-139">Utilizzo di hello metodo Round Robin di distribuzione dei dati è molto come sembra.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-139">Using hello Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="3ab1a-140">I dati vengono caricati, ogni riga viene semplicemente inviato toohello successiva distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-140">As your data is loaded, each row is simply sent toohello next distribution.</span></span>  <span data-ttu-id="3ab1a-141">Questo metodo di distribuzione dei dati hello distribuirà sempre in modo casuale dati hello molto in modo uniforme in tutte le distribuzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-141">This method of distributing hello data will always randomly distribute hello data very evenly across all of hello distributions.</span></span>  <span data-ttu-id="3ab1a-142">Non vi è alcun ordinamento eseguite durante hello round robin processo che inserisce i dati.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-142">That is, there is no sorting done during hello round robin process which places your data.</span></span>  <span data-ttu-id="3ab1a-143">Per questo motivo, una distribuzione round robin viene a volte definita hash causale.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="3ab1a-144">Con una tabella di round robin distribuita non contiene dati di hello toounderstand di necessità.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-144">With a round-robin distributed table there is no need toounderstand hello data.</span></span>  <span data-ttu-id="3ab1a-145">Per questo motivo le tabelle round robin sono spesso un'ottima scelta come destinazioni di caricamento.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="3ab1a-146">Per impostazione predefinita, se nessun metodo di distribuzione scelto, hello metodo distribuzione round robin verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-146">By default, if no distribution method is chosen, hello round robin distribution method will be used.</span></span>  <span data-ttu-id="3ab1a-147">Tuttavia, mentre il round robin tabelle sono toouse facile, perché in modo casuale i dati vengono distribuiti attraverso il sistema hello che significa che il sistema di hello non può garantire quali distribuzione ogni riga è in.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-147">However, while round robin tables are easy toouse, because data is randomly distributed across hello system it means that hello system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="3ab1a-148">Come un risultato di un sistema hello talvolta tooinvoke un toobetter di operazione di spostamento dati è necessario organizzare i dati prima che possa risolvere una query.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-148">As a result, hello system sometimes needs tooinvoke a data movement operation toobetter organize your data before it can resolve a query.</span></span>  <span data-ttu-id="3ab1a-149">Questo passaggio aggiuntivo può rallentare le query.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="3ab1a-150">Utilizzare la distribuzione Round Robin per la tabella in hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="3ab1a-150">Consider using Round Robin distribution for your table in hello following scenarios:</span></span>

* <span data-ttu-id="3ab1a-151">Quando si inizia come punto di partenza semplice.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="3ab1a-152">Se non è presente una chiave di join ovvia.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="3ab1a-153">Se non è presente la colonna buon candidato per la distribuzione di tabella hello hash</span><span class="sxs-lookup"><span data-stu-id="3ab1a-153">If there is not good candidate column for hash distributing hello table</span></span>
* <span data-ttu-id="3ab1a-154">Se hello tabella non condivide una chiave di join comune con altre tabelle</span><span class="sxs-lookup"><span data-stu-id="3ab1a-154">If hello table does not share a common join key with other tables</span></span>
* <span data-ttu-id="3ab1a-155">Se il join hello è meno significativo di altri join nella query hello</span><span class="sxs-lookup"><span data-stu-id="3ab1a-155">If hello join is less significant than other joins in hello query</span></span>
* <span data-ttu-id="3ab1a-156">Quando la tabella hello è una tabella temporanea di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="3ab1a-156">When hello table is a temporary staging table</span></span>

<span data-ttu-id="3ab1a-157">Entrambi gli esempi seguenti creano una tabella round robin:</span><span class="sxs-lookup"><span data-stu-id="3ab1a-157">Both of these examples will create a Round Robin Table:</span></span>

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
> <span data-ttu-id="3ab1a-158">Mentre il round robin è di tipo di tabella predefinito hello è esplicito nell'istruzione DDL è considerata buona norma in modo da deselezionare tooothers intenzioni hello del layout tabella.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-158">While round robin is hello default table type being explicit in your DDL is considered a best practice so that hello intentions of your table layout are clear tooothers.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="3ab1a-159">Tabelle con distribuzione hash</span><span class="sxs-lookup"><span data-stu-id="3ab1a-159">Hash Distributed Tables</span></span>
<span data-ttu-id="3ab1a-160">Utilizzando un **Hash distribuita** toodistribute algoritmo delle tabelle è possono migliorare le prestazioni per molti scenari riducendo lo spostamento dei dati in fase di query.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-160">Using a **Hash distributed** algorithm toodistribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="3ab1a-161">Hash distribuite sono tabelle che sono divise tra hello distribuiti database utilizzando un algoritmo di hash su una singola colonna che può essere selezionato.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-161">Hash distributed tables are tables which are divided between hello distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="3ab1a-162">colonna di distribuzione Hello è determina la modalità di suddivisione dati hello tra i database distribuiti.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-162">hello distribution column is what determines how hello data is divided across your distributed databases.</span></span>  <span data-ttu-id="3ab1a-163">funzione hash Hello utilizza hello distribuzione colonna tooassign righe toodistributions.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-163">hello hash function uses hello distribution column tooassign rows toodistributions.</span></span>  <span data-ttu-id="3ab1a-164">algoritmo di hash Hello e distribuzione risulta è deterministica.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-164">hello hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="3ab1a-165">Vale a dire hello stesso valore con tipo di dati verrà sempre hello è toohello stessa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-165">That is hello same value with hello same data type will always has toohello same distribution.</span></span>    

<span data-ttu-id="3ab1a-166">Questo esempio permette di creare una tabella distribuita:</span><span class="sxs-lookup"><span data-stu-id="3ab1a-166">This example will create a table distributed on id:</span></span>

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

## <a name="select-distribution-column"></a><span data-ttu-id="3ab1a-167">Selezionare la colonna di distribuzione</span><span class="sxs-lookup"><span data-stu-id="3ab1a-167">Select distribution column</span></span>
<span data-ttu-id="3ab1a-168">Quando si sceglie troppo**hash distribuire** una tabella, sarà necessario tooselect una colonna singola distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-168">When you choose too**hash distribute** a table, you will need tooselect a single distribution column.</span></span>  <span data-ttu-id="3ab1a-169">Quando si seleziona una colonna di distribuzione, sono disponibili tre tooconsider alcuni dei fattori principali.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-169">When selecting a distribution column, there are three major factors tooconsider.</span></span>  

<span data-ttu-id="3ab1a-170">Selezionare una singola colonna:</span><span class="sxs-lookup"><span data-stu-id="3ab1a-170">Select a single column which will:</span></span>

1. <span data-ttu-id="3ab1a-171">da non aggiornare,</span><span class="sxs-lookup"><span data-stu-id="3ab1a-171">Not be updated</span></span>
2. <span data-ttu-id="3ab1a-172">per distribuire i dati in modo uniforme, evitando asimmetrie,</span><span class="sxs-lookup"><span data-stu-id="3ab1a-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="3ab1a-173">per ridurre al minimo lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="3ab1a-174">Selezionare una colonna di distribuzione da non aggiornare</span><span class="sxs-lookup"><span data-stu-id="3ab1a-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="3ab1a-175">Le colonne di distribuzione non sono aggiornabili. Occorre quindi selezionare una colonna con valori statici.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="3ab1a-176">Se una colonna sarà necessario toobe aggiornato, non è in genere un candidato di distribuzione valide.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-176">If a column will need toobe updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="3ab1a-177">Se un caso in cui è necessario aggiornare una colonna di distribuzione, si possono eseguire innanzitutto l'eliminazione di riga hello e quindi inserendo una nuova riga.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-177">If there is a case where you must update a distribution column, this can be done by first deleting hello row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="3ab1a-178">Selezionare una colonna di distribuzione per distribuire i dati in modo uniforme</span><span class="sxs-lookup"><span data-stu-id="3ab1a-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="3ab1a-179">Dal momento che un sistema distribuito esegue solo il più rapidamente la distribuzione più lenta, è importante toodivide hello lavoro in modo uniforme tra distribuzioni hello in ordine tooachieve bilanciato esecuzione attraverso il sistema hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-179">Since a distributed system performs only as fast as its slowest distribution, it is important toodivide hello work evenly across hello distributions in order tooachieve balanced execution across hello system.</span></span>  <span data-ttu-id="3ab1a-180">modo Hello lavoro hello è suddivisa in un sistema distribuito è basato su dove si trovano dati hello per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-180">hello way hello work is divided on a distributed system is based on where hello data for each distribution lives.</span></span>  <span data-ttu-id="3ab1a-181">Questo rende una colonna di destra distribuzione hello tooselect molto importante per la distribuzione dei dati di hello in modo che ogni distribuzione ha lavoro uguale e verrà take hello toocomplete tempo stesso la propria parte del lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-181">This makes it very important tooselect hello right distribution column for distributing hello data so that each distribution has equal work and will take hello same time toocomplete its portion of hello work.</span></span>  <span data-ttu-id="3ab1a-182">Quando lavoro viene diviso e sistema hello, dati hello viene bilanciati tra le distribuzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-182">When work is well divided across hello system, hello data is balanced across hello distributions.</span></span>  <span data-ttu-id="3ab1a-183">Quando i dati non sono bilanciati in modo uniforme, si parla di **differenze di dati**.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="3ab1a-184">toodivide dati in modo uniforme ed evitare dati inclinazione, considerare i seguenti hello quando si seleziona la colonna di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="3ab1a-184">toodivide data evenly and avoid data skew, consider hello following when selecting your distribution column:</span></span>

1. <span data-ttu-id="3ab1a-185">Selezionare una colonna che contiene un numero significativo di valori distinct.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="3ab1a-186">Evitare di distribuire dati in colonne con pochi valori distinti.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="3ab1a-187">Evitare di distribuire dati in colonne con una frequenza elevata di valori Null.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="3ab1a-188">Evitare di distribuire i dati in colonne data.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="3ab1a-189">Poiché ogni valore con hash too1 delle distribuzioni di 60, la distribuzione uniforme tooachieve è tooselect una colonna che è altamente univoco e contiene più di 60 valori univoci.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-189">Since each value is hashed too1 of 60 distributions, tooachieve even distribution you will want tooselect a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="3ab1a-190">tooillustrate, si consideri il caso in cui una colonna dispone solo valori univoci 40.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-190">tooillustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="3ab1a-191">Se questa colonna è stata selezionata come chiave di distribuzione hello, dati hello per la tabella verrebbero reindirizzato 40 distribuzioni al massimo, lasciando 20 distribuzioni con alcun dato e non toodo l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-191">If this column was selected as hello distribution key, hello data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing toodo.</span></span>  <span data-ttu-id="3ab1a-192">Al contrario, hello altre 40 distribuzioni sarebbe necessario più lavoro toodo, che se hello dati è stata distribuiti uniformemente le distribuzioni di più di 60.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-192">Conversely, hello other 40 distributions would have more work toodo that if hello data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="3ab1a-193">Questo scenario è un esempio di differenza di dati.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="3ab1a-194">Nel sistema MPP, ogni passaggio della query è in attesa per tutte le distribuzioni toocomplete della quota di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-194">In MPP system, each query step waits for all distributions toocomplete their share of hello work.</span></span>  <span data-ttu-id="3ab1a-195">Se una distribuzione è più operazioni rispetto ad altri utenti hello, hello risorse di hello altre distribuzioni sono essenzialmente sprecati in attesa solo su distribuzione occupato hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-195">If one distribution is doing more work than hello others, then hello resource of hello other distributions are essentially wasted just waiting on hello busy distribution.</span></span>  <span data-ttu-id="3ab1a-196">Quando si lavoro non viene distribuito uniformemente tra tutte le distribuzioni, si parla di **differenza di elaborazioni**.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="3ab1a-197">Elaborazione inclinazione causerà toorun query inferiore se il carico di lavoro hello può essere distribuito uniformemente in distribuzioni hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-197">Processing skew will cause queries toorun slower than if hello workload can be evenly spread across hello distributions.</span></span>  <span data-ttu-id="3ab1a-198">Lo sfasamento dei segnali dati comporti tooprocessing inclinazione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-198">Data skew will lead tooprocessing skew.</span></span>

<span data-ttu-id="3ab1a-199">Evitare di distribuire nella colonna elevata ammette valori null come valori null hello verranno tutte inserite in hello stessa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-199">Avoid distributing on highly nullable column as hello null values will all land on hello same distribution.</span></span> <span data-ttu-id="3ab1a-200">La distribuzione di una colonna della data può essere causato anche l'elaborazione di inclinazione perché tutti i dati per una data specificata verranno inserite in hello stessa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-200">Distributing on a date column can also cause processing skew because all data for a given date will land on hello same distribution.</span></span> <span data-ttu-id="3ab1a-201">Se più utenti eseguono query filtraggio tutti in hello stessa data, quindi solo 1 delle distribuzioni di 60 hello prevede di effettuare tutto il lavoro hello dopo una data specificata verranno solo su una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-201">If several users are executing queries all filtering on hello same date, then only 1 of hello 60 distributions will be doing all of hello work since a given date will only be on one distribution.</span></span> <span data-ttu-id="3ab1a-202">In questo scenario, le query hello probabilmente eseguirà 60 volte inferiore se i dati di hello ugualmente sono stati distribuiti su tutte le distribuzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-202">In this scenario, hello queries will likely run 60 times slower than if hello data were equally spread over all of hello distributions.</span></span>

<span data-ttu-id="3ab1a-203">Quando non esiste alcuna colonna candidato ideale, quindi utilizzare round robin come metodo di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-203">When no good candidate columns exist, then consider using round robin as hello distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="3ab1a-204">Selezionare una colonna di distribuzione per ridurre al minimo lo spostamento dei dati</span><span class="sxs-lookup"><span data-stu-id="3ab1a-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="3ab1a-205">Ridurre al minimo lo spostamento di dati selezionando una colonna di destra distribuzione hello è una delle strategie più importanti di hello per ottimizzare le prestazioni del proprio SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-205">Minimizing data movement by selecting hello right distribution column is one of hello most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="3ab1a-206">In genere lo spostamento dei dati si verifica quando le tabelle vengono unite in join o vengono eseguite aggregazioni.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="3ab1a-207">Le colonne usate nelle clausole `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` e `HAVING` sono **ottimi** candidati per la distribuzione hash.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="3ab1a-208">Hello d'altro canto, le colonne in hello `WHERE` eseguire clausola **non** effettuare per i candidati colonna hash valida perché limitano le distribuzioni partecipano a query hello, che causa l'elaborazione inclinazione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-208">On hello other hand, columns in hello `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in hello query, causing processing skew.</span></span>  <span data-ttu-id="3ab1a-209">Un buon esempio di una colonna che potrebbe essere tentati toodistribute, ma spesso può causare l'inclinazione di elaborazione è una colonna di date.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-209">A good example of a column which might be tempting toodistribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="3ab1a-210">In generale, se si dispone di due tabelle dei fatti di grandi dimensioni interessate di frequente in un join, sarà possibile ottenere hello la maggior parte delle prestazioni tramite la distribuzione di entrambe le tabelle in una delle colonne di join hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain hello most performance by distributing both tables on one of hello join columns.</span></span>  <span data-ttu-id="3ab1a-211">Se si dispone di una tabella che non viene mai tooanother unita in join nella tabella dei fatti di grandi dimensioni, quindi cercare toocolumns che si trovano spesso in hello `GROUP BY` clausola.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-211">If you have a table that is never joined tooanother large fact table, then look toocolumns that are frequently in hello `GROUP BY` clause.</span></span>

<span data-ttu-id="3ab1a-212">Esistono alcuni criteri di chiave che devono essere soddisfatto tooavoid lo spostamento di dati durante un join:</span><span class="sxs-lookup"><span data-stu-id="3ab1a-212">There are a few key criteria which must be met tooavoid data movement during a join:</span></span>

1. <span data-ttu-id="3ab1a-213">Hello tabelle unite in join hello devono essere distribuito su hash **uno** di colonne hello che fanno parte di join hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-213">hello tables involved in hello join must be hash distributed on **one** of hello columns participating in hello join.</span></span>
2. <span data-ttu-id="3ab1a-214">i tipi di dati delle colonne di join hello Hello di entrambe le tabelle devono essere uguali.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-214">hello data types of hello join columns must match between both tables.</span></span>
3. <span data-ttu-id="3ab1a-215">colonne di Hello devono essere aggiunti con un operatore di uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-215">hello columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="3ab1a-216">Hello join tipo non può essere un `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-216">hello join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="3ab1a-217">Risoluzione dei problemi relativi alle asimmetrie dei dati</span><span class="sxs-lookup"><span data-stu-id="3ab1a-217">Troubleshooting data skew</span></span>
<span data-ttu-id="3ab1a-218">Quando i dati della tabella vengono distribuiti con metodo di distribuzione hash hello è possibile che alcune distribuzioni saranno sfasato toohave eccessivamente più dati rispetto ad altri.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-218">When table data is distributed using hello hash distribution method there is a chance that some distributions will be skewed toohave disproportionately more data than others.</span></span> <span data-ttu-id="3ab1a-219">Eccessivi dati sfasamento del possono influire sulle prestazioni delle query, perché il risultato finale di hello di una query distribuita deve attendere toofinish distribuzione in esecuzione più lunga di hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-219">Excessive data skew can impact query performance because hello final result of a distributed query must wait for hello longest running distribution toofinish.</span></span> <span data-ttu-id="3ab1a-220">In base al grado hello di dati hello inclinazione che potrebbe essere necessario tooaddress.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-220">Depending on hello degree of hello data skew you might need tooaddress it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="3ab1a-221">Identificazione dell'asimmetria dei dati</span><span class="sxs-lookup"><span data-stu-id="3ab1a-221">Identifying skew</span></span>
<span data-ttu-id="3ab1a-222">Tooidentify un modo semplice una tabella come asimmetrica è toouse `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-222">A simple way tooidentify a table as skewed is toouse `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="3ab1a-223">Si tratta di un modo molto rapido e semplice di toosee hello numero di righe della tabella che vengono archiviati in ognuna delle distribuzioni di hello 60 del database.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-223">This is a very quick and simple way toosee hello number of table rows that are stored in each of hello 60 distributions of your database.</span></span>  <span data-ttu-id="3ab1a-224">Tenere presente che per ottenere prestazioni più bilanciato hello, righe hello nella tabella distribuita devono essere suddivise in modo uniforme tra tutte le distribuzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-224">Remember that for hello most balanced performance, hello rows in your distributed table should be spread evenly across all hello distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="3ab1a-225">Tuttavia, se si esegue una query viste a gestione dinamica hello Azure SQL Data Warehouse (DMV) è possibile eseguire un'analisi più dettagliata.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-225">However, if you query hello Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="3ab1a-226">toostart, creare la vista hello [dbo.vTableSizes] [ dbo.vTableSizes] visualizzare utilizzando hello SQL da [Cenni preliminari su tabella] [ Overview] articolo.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-226">toostart, create hello view [dbo.vTableSizes][dbo.vTableSizes] view using hello SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="3ab1a-227">Una volta hello vista viene creata, eseguire questa query tooidentify quali tabelle presentano più di 10% dati inclinazione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-227">Once hello view is created, run this query tooidentify which tables have more than 10% data skew.</span></span>

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

### <a name="resolving-data-skew"></a><span data-ttu-id="3ab1a-228">Risoluzione delle asimmetrie di distribuzione</span><span class="sxs-lookup"><span data-stu-id="3ab1a-228">Resolving data skew</span></span>
<span data-ttu-id="3ab1a-229">Non tutti inclinazione è sufficiente toowarrant una correzione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-229">Not all skew is enough toowarrant a fix.</span></span>  <span data-ttu-id="3ab1a-230">In alcuni casi, le prestazioni di hello di una tabella in alcune query possono annullare danni hello dei dati di inclinazione.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-230">In some cases, hello performance of a table in some queries can outweigh hello harm of data skew.</span></span>  <span data-ttu-id="3ab1a-231">toodecide se è necessario risolvere i dati dello sfasamento dei segnali in una tabella, è necessario comprendere quanto possibile sui volumi di dati hello e query nel carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-231">toodecide if you should resolve data skew in a table, you should understand as much as possible about hello data volumes and queries in your workload.</span></span>   <span data-ttu-id="3ab1a-232">Un modo toolook impatto hello di inclinazione è passaggi hello toouse hello [Query monitoraggio] [ Query Monitoring] articolo impatto hello toomonitor di inclinazione sulle prestazioni delle query e in particolare hello query lunghe toohow di impatto richiedere toocomplete in distribuzioni di singoli hello.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-232">One way toolook at hello impact of skew is toouse hello steps in hello [Query Monitoring][Query Monitoring] article toomonitor hello impact of skew on query performance and specifically hello impact toohow long queries take toocomplete on hello individual distributions.</span></span>

<span data-ttu-id="3ab1a-233">Distribuzione dei dati è una questione di ricerca hello giusto equilibrio riducendo al minimo lo sfasamento dei segnali dati e ridurre al minimo lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-233">Distributing data is a matter of finding hello right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="3ab1a-234">Questi possono essere opposte obiettivi e talvolta potrebbe essere necessario tookeep dati inclinazione nello spostamento dei dati tooreduce di ordine.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-234">These can be opposing goals, and sometimes you will want tookeep data skew in order tooreduce data movement.</span></span> <span data-ttu-id="3ab1a-235">Ad esempio, quando la colonna di distribuzione hello è spesso hello condiviso colonna join e aggregazioni, si verrà essere riducendo al minimo lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-235">For example, when hello distribution column is frequently hello shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="3ab1a-236">Hello c'è lo spostamento dei dati minimi hello superiore a quello previsto impatto hello di avere dati dello sfasamento dei segnali.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-236">hello benefit of having hello minimal data movement might outweigh hello impact of having data skew.</span></span>

<span data-ttu-id="3ab1a-237">un tipico di Hello tooresolve dati inclinazione è toore-creare hello tabella con una colonna di distribuzione diverso.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-237">hello typical way tooresolve data skew is toore-create hello table with a different distribution column.</span></span> <span data-ttu-id="3ab1a-238">Poiché non esiste alcun modo toochange hello distribuzione colonna esistente, hello modo toochange hello distribuzione tabelle di una tabella è toorecreate con un [] [un'istruzione CTAS].</span><span class="sxs-lookup"><span data-stu-id="3ab1a-238">Since there is no way toochange hello distribution column on an existing table, hello way toochange hello distribution of a table it toorecreate it with a [CTAS][].</span></span>  <span data-ttu-id="3ab1a-239">Di seguito sono riportati due esempi di risoluzione di distribuzioni asimmetriche dei dati:</span><span class="sxs-lookup"><span data-stu-id="3ab1a-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a><span data-ttu-id="3ab1a-240">Esempio 1: Creare nuovamente la tabella hello con una nuova colonna di distribuzione</span><span class="sxs-lookup"><span data-stu-id="3ab1a-240">Example 1: Re-create hello table with a new distribution column</span></span>
<span data-ttu-id="3ab1a-241">Questo esempio viene utilizzata [un'istruzione CTAS] [] toore-creare una tabella con una colonna di distribuzione hash diverso.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-241">This example uses [CTAS][] toore-create a table with a different hash distribution column.</span></span>

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

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a><span data-ttu-id="3ab1a-242">Esempio 2: Creare nuovamente tabella hello utilizzando la distribuzione round robin</span><span class="sxs-lookup"><span data-stu-id="3ab1a-242">Example 2: Re-create hello table using round robin distribution</span></span>
<span data-ttu-id="3ab1a-243">Questo esempio viene utilizzata [un'istruzione CTAS] [] toore-creare una tabella con round robin anziché una distribuzione di hash.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-243">This example uses [CTAS][] toore-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="3ab1a-244">Questa modifica provocherà la distribuzione di dati anche a costo di hello spostamento dei dati maggiore.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-244">This change will produce even data distribution at hello cost of increased data movement.</span></span>

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

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="3ab1a-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3ab1a-245">Next steps</span></span>
<span data-ttu-id="3ab1a-246">toolearn ulteriori informazioni su progettazione della tabella, vedere hello [Distribuisci][Distribute], [indice][Index], [partizione] [ Partition], [Tipi di dati][Data Types], [statistiche] [ Statistics] e [tabelle temporanee] [ Temporary] articoli.</span><span class="sxs-lookup"><span data-stu-id="3ab1a-246">toolearn more about table design, see hello [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="3ab1a-247">Per una panoramica delle procedure consigliate, vedere [Procedure consigliate per SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="3ab1a-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
