---
title: Tecnologie in memoria del database SQL di Azure | Documentazione Microsoft
description: Le tecnologie in memoria del database SQL di Azure migliorano notevolmente le prestazioni dei carichi di lavoro transazionali e analitici. Informazioni su come sfruttare i vantaggi di queste tecnologie.
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 4cb45551c486263f26947e5684d54b4f2ecc7410
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="69e37-104">Ottimizzare le prestazioni tramite le tecnologie in memoria nel database SQL</span><span class="sxs-lookup"><span data-stu-id="69e37-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="69e37-105">Tramite le tecnologie in memoria del database SQL di Azure, è possibile migliorare le prestazioni di diversi carichi di lavoro: transazionale (elaborazione transazionale online o OLTP), analitica (elaborazione analitica online o OLAP) e mista (elaborazione ibrida transazione/analitica o HTAP).</span><span class="sxs-lookup"><span data-stu-id="69e37-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="69e37-106">Grazie a una più efficiente elaborazione delle query e delle transazioni, le tecnologie in memoria aiutano a ridurre i costi.</span><span class="sxs-lookup"><span data-stu-id="69e37-106">Because of the more efficient query and transaction processing, In-Memory technologies also help you to reduce cost.</span></span> <span data-ttu-id="69e37-107">In genere non è necessario aggiornare il piano tariffario del database per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="69e37-107">You typically don't need to upgrade the pricing tier of the database to achieve performance gains.</span></span> <span data-ttu-id="69e37-108">In alcuni casi infatti le tecnologie in memoria consentono di ridurre il piano tariffario e di osservare al contempo miglioramenti delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="69e37-108">In some cases, you might even be able reduce the pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="69e37-109">Di seguito sono riportati due esempi che mostrano come la tecnologia OLTP in memoria abbia contribuito a migliorare significativamente le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="69e37-109">Here are two examples of how In-Memory OLTP helped to significantly improve performance:</span></span>

- <span data-ttu-id="69e37-110">Sfruttando la tecnologia OLTP in memoria [Quorum Business Solutions è riuscita a raddoppiare il carico di lavoro migliorando i valori DTU del 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="69e37-110">By using In-Memory OLTP, [Quorum Business Solutions was able to double their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="69e37-111">DTU significa *unità di velocità effettiva database* e include una misurazione del consumo di risorse.</span><span class="sxs-lookup"><span data-stu-id="69e37-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="69e37-112">Il video seguente illustra un miglioramento significativo nell'uso delle risorse con un carico di lavoro di esempio: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (Video su OLTP in memoria nel database SQL di Azure).</span><span class="sxs-lookup"><span data-stu-id="69e37-112">The following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="69e37-113">Per altre informazioni, vedere il post di blog: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/) (Post di blog su OLTP nel database SQL di Azure)</span><span class="sxs-lookup"><span data-stu-id="69e37-113">For more details, see the blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="69e37-114">Le tecnologie in memoria sono disponibili in tutti i database nel livello Premium, inclusi i database nei pool elastici Premium.</span><span class="sxs-lookup"><span data-stu-id="69e37-114">In-Memory technologies are available in all databases in the Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="69e37-115">Il video seguente spiega il potenziale miglioramento delle prestazioni con le tecnologie in memoria nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="69e37-115">The following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="69e37-116">Tenere presente che il miglioramento delle prestazioni dipende sempre da numerosi fattori, tra cui la natura del carico di lavoro e dei dati, il modello di accesso del database e così via.</span><span class="sxs-lookup"><span data-stu-id="69e37-116">Remember that the performance gain that you see always depends on many factors, including the nature of the workload and data, access pattern of the database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="69e37-117">Il database SQL di Azure dispone delle seguenti tecnologie in memoria:</span><span class="sxs-lookup"><span data-stu-id="69e37-117">Azure SQL Database has the following In-Memory technologies:</span></span>

- <span data-ttu-id="69e37-118">*OLTP in memoria*: aumenta la velocità effettiva e riduce la latenza per l'elaborazione delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="69e37-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="69e37-119">Gli scenari che beneficiano dell'OLTP in memoria sono: elaborazione transazionale ad alta velocità di elaborazione, come l'inserimento di dati commerciali e da videogiochi, da eventi o dispositivi IoT, il caching, il caricamento di dati, le tabelle temporanee e gli scenari con variabili di tabella.</span><span class="sxs-lookup"><span data-stu-id="69e37-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="69e37-120">Gli *indici columnstore cluster* riducono fino a 10 volte il footprint della memoria e migliorano le prestazioni delle query di reporting e analisi.</span><span class="sxs-lookup"><span data-stu-id="69e37-120">*Clustered columnstore indexes* reduce your storage footprint (up to 10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="69e37-121">È possibile usare gli indici con tabelle dei fatti nei data mart per inserire più dati nel database e migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="69e37-121">You can use it with fact tables in your data marts to fit more data in your database and improve performance.</span></span> <span data-ttu-id="69e37-122">Gli indici possono anche essere usati con i dati cronologici nel database operativo per archiviare ed essere in grado di eseguire una query su una quantità di dati 10 volte superiore.</span><span class="sxs-lookup"><span data-stu-id="69e37-122">Also, you can use it with historical data in your operational database to archive and be able to query up to 10 times more data.</span></span>
- <span data-ttu-id="69e37-123">Gli *indici columnstore non cluster* per HTAP consentono di ottenere in tempo reale informazioni approfondite sull'azienda eseguendo una query direttamente sul database operativo, senza la necessità di eseguire un processo ETL dispendioso e attendere che il data warehouse venga popolato.</span><span class="sxs-lookup"><span data-stu-id="69e37-123">*Nonclustered columnstore indexes* for HTAP help you to gain real-time insights into your business through querying the operational database directly, without the need to run an expensive extract, transform, and load (ETL) process and wait for the data warehouse to be populated.</span></span> <span data-ttu-id="69e37-124">Gli indici columnstore non cluster consentono l'esecuzione molto rapida delle query di analisi nei database OLTP, riducendo l'impatto sul carico di lavoro operativo.</span><span class="sxs-lookup"><span data-stu-id="69e37-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on the OLTP database, while reducing the impact on the operational workload.</span></span>
- <span data-ttu-id="69e37-125">È possibile anche disporre di una tabella ottimizzata per la memoria con un indice columnstore.</span><span class="sxs-lookup"><span data-stu-id="69e37-125">You can also have the combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="69e37-126">Tale combinazione consente di elaborare le transazioni e *al contempo* di eseguire le query di analisi sugli stessi dati in tempi estremamente rapidi.</span><span class="sxs-lookup"><span data-stu-id="69e37-126">This combination enables you to perform very fast transaction processing, and to *concurrently* run analytics queries very quickly on the same data.</span></span>

<span data-ttu-id="69e37-127">Gli indici columnstore e OLTP in memoria fanno parte di SQL Server rispettivamente dal 2012 e dal 2014.</span><span class="sxs-lookup"><span data-stu-id="69e37-127">Both columnstore indexes and In-Memory OLTP have been part of the SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="69e37-128">Il database SQL di Azure e SQL Server condividono la stessa implementazione delle tecnologie in memoria.</span><span class="sxs-lookup"><span data-stu-id="69e37-128">Azure SQL Database and SQL Server share the same implementation of In-Memory technologies.</span></span> <span data-ttu-id="69e37-129">In futuro, le nuove funzionalità per queste tecnologie verranno integrate prima nel database SQL di Azure e poi in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="69e37-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="69e37-130">Questo argomento descrive gli aspetti di OLTP in memoria e degli indici columnstore specifici del database SQL di Azure e include alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="69e37-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific to Azure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="69e37-131">Viene analizzato l'impatto di queste tecnologie sulla memoria e i limiti sulle dimensioni dei dati.</span><span class="sxs-lookup"><span data-stu-id="69e37-131">You'll see the impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="69e37-132">Verrà illustrato come gestire lo spostamento dei database che sfruttano queste tecnologie tra i diversi piani tariffari.</span><span class="sxs-lookup"><span data-stu-id="69e37-132">You'll see how to manage the movement of databases that use these technologies between the different pricing tiers.</span></span>
- <span data-ttu-id="69e37-133">Verranno esaminati due esempi che illustrano l'uso di OLTP in memoria e degli indici columnstore nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="69e37-133">You'll see two samples that illustrate the use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="69e37-134">Per altre informazioni, vedere le risorse seguenti.</span><span class="sxs-lookup"><span data-stu-id="69e37-134">See the following resources for more information.</span></span>

<span data-ttu-id="69e37-135">Approfondimento sulle tecnologie:</span><span class="sxs-lookup"><span data-stu-id="69e37-135">In-depth information about the technologies:</span></span>

- <span data-ttu-id="69e37-136">[Panoramica e scenari di utilizzo](https://msdn.microsoft.com/library/mt774593.aspx), inclusi riferimenti a casi di studio sui clienti e informazioni introduttive</span><span class="sxs-lookup"><span data-stu-id="69e37-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references to customer case studies and information to get started)</span></span>
- [<span data-ttu-id="69e37-137">OLTP in memoria</span><span class="sxs-lookup"><span data-stu-id="69e37-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="69e37-138">Descrizione degli indici columnstore</span><span class="sxs-lookup"><span data-stu-id="69e37-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="69e37-139">L'elaborazione analitica e transazionale ibrida (HTAP), anche nota come [analisi operativa in tempo reale](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="69e37-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="69e37-140">Nozioni di base sull'OLTP in memoria: [Avvio rapido 1: Tecnologie OLTP in memoria per ottimizzare le prestazioni di T-SQL](http://msdn.microsoft.com/library/mt694156.aspx), un altro articolo introduttivo</span><span class="sxs-lookup"><span data-stu-id="69e37-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article to help you get started)</span></span>

<span data-ttu-id="69e37-141">Video di approfondimento sulle tecnologie:</span><span class="sxs-lookup"><span data-stu-id="69e37-141">In-depth videos about the technologies:</span></span>

- <span data-ttu-id="69e37-142">[OLTP in memoria nel database SQL di Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB), che contiene una demo dei vantaggi in termini di prestazioni e i passaggi per riprodurre tali risultati manualmente</span><span class="sxs-lookup"><span data-stu-id="69e37-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps to reproduce these results yourself)</span></span>
- [<span data-ttu-id="69e37-143">Video OLTP in memoria: Che cos'è e come/quando usarlo</span><span class="sxs-lookup"><span data-stu-id="69e37-143">In-Memory OLTP Videos: What it is and When/How to use it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="69e37-144">Indice ColumnStore: Video sull'analisi in memoria da Ignite 2016</span><span class="sxs-lookup"><span data-stu-id="69e37-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="69e37-145">Dimensioni di archiviazione e dati</span><span class="sxs-lookup"><span data-stu-id="69e37-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="69e37-146">Limite su dimensioni dei dati e archiviazione per OLTP in memoria</span><span class="sxs-lookup"><span data-stu-id="69e37-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="69e37-147">OLTP in memoria include tabelle con ottimizzazione per la memoria, che vengono usate per archiviare i dati utente.</span><span class="sxs-lookup"><span data-stu-id="69e37-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="69e37-148">Queste tabelle devono rientrare nella memoria.</span><span class="sxs-lookup"><span data-stu-id="69e37-148">These tables are required to fit in memory.</span></span> <span data-ttu-id="69e37-149">Poiché la memoria è gestita direttamente nel servizio del database SQL, esiste il concetto di quota per i dati utente.</span><span class="sxs-lookup"><span data-stu-id="69e37-149">Because you manage memory directly in the SQL Database service, we have the  concept of a quota for user data.</span></span> <span data-ttu-id="69e37-150">Questo concetto è definito *archiviazione di OLTP in memoria*.</span><span class="sxs-lookup"><span data-stu-id="69e37-150">This idea is referred to as *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="69e37-151">Ogni piano tariffario relativo a database autonomi e pool elastici supportati include una certa quantità di spazio di archiviazione OLTP in memoria.</span><span class="sxs-lookup"><span data-stu-id="69e37-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="69e37-152">Al momento della redazione di questo articolo, è disponibile un gigabyte di spazio di archiviazione per ogni 125 unità di transazione di database (DTU) o unità di transazione di database elastico (eDTU).</span><span class="sxs-lookup"><span data-stu-id="69e37-152">At the time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="69e37-153">L'articolo sui [Livelli di servizio del database SQL](sql-database-service-tiers.md) contiene l'elenco ufficiale dello spazio di archiviazione OLTP in memoria disponibile per ogni piano tariffario di database autonomi e pool elastici supportati.</span><span class="sxs-lookup"><span data-stu-id="69e37-153">The [SQL Database service tiers](sql-database-service-tiers.md) article has the official list of the In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="69e37-154">Gli elementi seguenti rientrano nel limite di archiviazione di OLTP in memoria:</span><span class="sxs-lookup"><span data-stu-id="69e37-154">The following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="69e37-155">Righe di dati utente attive nelle tabelle con ottimizzazione per la memoria e variabili di tabella.</span><span class="sxs-lookup"><span data-stu-id="69e37-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="69e37-156">Si noti che le versioni precedenti della riga non vengono conteggiate nel limite.</span><span class="sxs-lookup"><span data-stu-id="69e37-156">Note that old row versions don't count toward the cap.</span></span>
- <span data-ttu-id="69e37-157">Indici nelle tabelle con ottimizzazione per la memoria.</span><span class="sxs-lookup"><span data-stu-id="69e37-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="69e37-158">Costi operativi delle operazioni ALTER TABLE.</span><span class="sxs-lookup"><span data-stu-id="69e37-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="69e37-159">Se si raggiunge il limite, si riceve un errore di superamento della quota e non sarà più possibile inserire o aggiornare dati.</span><span class="sxs-lookup"><span data-stu-id="69e37-159">If you hit the cap, you receive an out-of-quota error, and you are no longer able to insert or update data.</span></span> <span data-ttu-id="69e37-160">Per risolvere il problema, eliminare i dati o aumentare il piano tariffario del database o del pool.</span><span class="sxs-lookup"><span data-stu-id="69e37-160">To mitigate this error, delete data or increase the pricing tier of the database or pool.</span></span>

<span data-ttu-id="69e37-161">Per dettagli sul monitoraggio dell'uso dello spazio di archiviazione OLTP in memoria e sulla configurazione degli avvisi al raggiungimento del limite, vedere [Monitorare l'archiviazione in memoria](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="69e37-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit the cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="69e37-162">Informazioni sui pool elastici</span><span class="sxs-lookup"><span data-stu-id="69e37-162">About elastic pools</span></span>

<span data-ttu-id="69e37-163">Con i pool elastici, lo spazio di archiviazione OLTP in memoria è condiviso tra tutti i database nel pool.</span><span class="sxs-lookup"><span data-stu-id="69e37-163">With elastic pools, the In-Memory OLTP storage is shared across all databases in the pool.</span></span> <span data-ttu-id="69e37-164">Ne consegue che l'utilizzo in un database può potenzialmente influire sugli altri database.</span><span class="sxs-lookup"><span data-stu-id="69e37-164">Therefore, the usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="69e37-165">Esistono due metodi per la risoluzione di questo problema:</span><span class="sxs-lookup"><span data-stu-id="69e37-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="69e37-166">Configurare Max-eDTU per i database con numero di eDTU inferiore rispetto al numero di eDTU per l'intero pool.</span><span class="sxs-lookup"><span data-stu-id="69e37-166">Configure a Max-eDTU for databases that is lower than the eDTU count for the pool as a whole.</span></span> <span data-ttu-id="69e37-167">Ciò limita l'uso dello spazio di archiviazione OLTP in memoria in qualsiasi database del pool alla dimensione corrispondente al numero di eDTU.</span><span class="sxs-lookup"><span data-stu-id="69e37-167">This maximum caps the In-Memory OLTP storage utilization, in any database in the pool, to the size that corresponds to the eDTU count.</span></span>
- <span data-ttu-id="69e37-168">Configurare Min-eDTU su un valore maggiore di 0.</span><span class="sxs-lookup"><span data-stu-id="69e37-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="69e37-169">In questo modo si garantisce che ogni database nel pool abbia a disposizione la quantità di spazio di archiviazione OLTP in memoria corrispondente al valore Min-eDTU configurato.</span><span class="sxs-lookup"><span data-stu-id="69e37-169">This minimum guarantees that each database in the pool has the amount of available In-Memory OLTP storage that corresponds to the configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="69e37-170">Dimensioni dei dati e archiviazione per gli indici columnstore</span><span class="sxs-lookup"><span data-stu-id="69e37-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="69e37-171">Gli indici columnstore non devono essere contenuti nella memoria.</span><span class="sxs-lookup"><span data-stu-id="69e37-171">Columnstore indexes aren't required to fit in memory.</span></span> <span data-ttu-id="69e37-172">L'unico limite alla dimensione degli indici è quindi la dimensione complessiva massima del database, descritta nell'articolo [Livelli di servizio del database SQL](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="69e37-172">Therefore, the only cap on the size of the indexes is the maximum overall database size, which is documented in the [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="69e37-173">Quando si usano gli indici columnstore cluster, viene impiegata la compressione a colonne per l'archiviazione delle tabelle di base.</span><span class="sxs-lookup"><span data-stu-id="69e37-173">When you use clustered columnstore indexes, columnar compression is used for the base table storage.</span></span> <span data-ttu-id="69e37-174">Ciò può ridurre notevolmente il footprint di archiviazione dei dati utente, ovvero è possibile inserire più dati nel database.</span><span class="sxs-lookup"><span data-stu-id="69e37-174">This compression can significantly reduce the storage footprint of your user data, which means that you can fit more data in the database.</span></span> <span data-ttu-id="69e37-175">Usando la [compressione a colonne dell'archivio](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression), è possibile inserire una quantità ancora maggiore di dati.</span><span class="sxs-lookup"><span data-stu-id="69e37-175">And the compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="69e37-176">La quantità di compressione che è possibile ottenere dipende dalla natura dei dati, ma generalmente si aggira intorno a 10 volte (10X) la compressione tradizionale.</span><span class="sxs-lookup"><span data-stu-id="69e37-176">The amount of compression that you can achieve depends on the nature of the data, but 10 times the compression is not uncommon.</span></span>

<span data-ttu-id="69e37-177">Ad esempio, se si dispone di un database con dimensioni massime di 1 terabyte (TB) e si raggiunge una compressione 10X tramite columnstore, nel database è possibile inserire un totale di 10 TB di dati utente.</span><span class="sxs-lookup"><span data-stu-id="69e37-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times the compression by using columnstore indexes, you can fit a total of 10 TB of user data in the database.</span></span>

<span data-ttu-id="69e37-178">Quando si usano indici columnstore non cluster, la tabella di base è ancora archiviata nel formato rowstore tradizionale.</span><span class="sxs-lookup"><span data-stu-id="69e37-178">When you use nonclustered columnstore indexes, the base table is still stored in the traditional rowstore format.</span></span> <span data-ttu-id="69e37-179">Pertanto, il risparmio di archiviazione non è paragonabile a quello ottenuto con gli indici columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="69e37-179">Therefore, the storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="69e37-180">Tuttavia, se si sostituisce un numero di indici non in cluster tradizionali con un indice columnstore singolo, è sempre possibile riscontrare un risparmio complessivo nel footprint della memoria per la tabella.</span><span class="sxs-lookup"><span data-stu-id="69e37-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in the storage footprint for the table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="69e37-181">Spostamento dei database tra i piani tariffari tramite tecnologie in memoria</span><span class="sxs-lookup"><span data-stu-id="69e37-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="69e37-182">Passando a un piano tariffario superiore, ad esempio da Standard a Premium, non si corre mai il rischio di incompatibilità o altri problemi.</span><span class="sxs-lookup"><span data-stu-id="69e37-182">There are never any incompatibilities or other problems when you upgrade to a higher pricing tier, such as from Standard to Premium.</span></span> <span data-ttu-id="69e37-183">Il passaggio implica semplicemente un aumento di funzionalità e risorse.</span><span class="sxs-lookup"><span data-stu-id="69e37-183">The available functionality and resources only increase.</span></span>

<span data-ttu-id="69e37-184">Tuttavia, eseguire il downgrade del piano tariffario può avere un impatto negativo sul database.</span><span class="sxs-lookup"><span data-stu-id="69e37-184">But downgrading the pricing tier can negatively impact your database.</span></span> <span data-ttu-id="69e37-185">Questo impatto è particolarmente evidente quando si effettua il downgrade da Premium a Standard o Basic nei casi in cui il database contenga oggetti di OLTP In memoria.</span><span class="sxs-lookup"><span data-stu-id="69e37-185">The impact is especially apparent when you downgrade from Premium to Standard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="69e37-186">Le tabelle ottimizzate per la memoria e gli indici columnstore non sono disponibili dopo il downgrade, anche se dovessero rimanere visibili.</span><span class="sxs-lookup"><span data-stu-id="69e37-186">Memory-optimized tables, and columnstore indexes, are unavailable after the downgrade (even if they remain visible).</span></span> <span data-ttu-id="69e37-187">Le stesse considerazioni si applicano quando si effettua il downgrade del piano tariffario di un pool elastico o quando si esegue lo spostamento dei database con tecnologie in memoria in un pool elastico Standard o Basic.</span><span class="sxs-lookup"><span data-stu-id="69e37-187">The same considerations apply when you're lowering the pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="69e37-188">OLTP in memoria</span><span class="sxs-lookup"><span data-stu-id="69e37-188">In-Memory OLTP</span></span>

<span data-ttu-id="69e37-189">*Downgrade a Basic/Standard*: OLTP in memoria non è supportato nei database del piano Standard o Basic.</span><span class="sxs-lookup"><span data-stu-id="69e37-189">*Downgrading to Basic/Standard*: In-Memory OLTP isn't supported in databases in the Standard or Basic tier.</span></span> <span data-ttu-id="69e37-190">Non è possibile spostare un database che contiene oggetti OLTP in memoria al piano tariffario Standard o Basic.</span><span class="sxs-lookup"><span data-stu-id="69e37-190">In addition, it isn't possible to move a database that has any In-Memory OLTP objects to the Standard or Basic tier.</span></span>

<span data-ttu-id="69e37-191">Prima di eseguire il downgrade del database al livello Standard o Basic, rimuovere tutti i tipi di tabella e le tabelle con ottimizzazione per la memoria, nonché tutti i moduli T-SQL compilati in modo nativo.</span><span class="sxs-lookup"><span data-stu-id="69e37-191">Before you downgrade the database to Standard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="69e37-192">Esiste un modo a livello di codice per capire se un determinato database supporta OLTP in memoria.</span><span class="sxs-lookup"><span data-stu-id="69e37-192">There is a programmatic way to understand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="69e37-193">È possibile eseguire la query Transact-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="69e37-193">You can execute the following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="69e37-194">Se la query restituisce **1**, OLTP in memoria è supportato nel database.</span><span class="sxs-lookup"><span data-stu-id="69e37-194">If the query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="69e37-195">*Downgrade a un livello Premium inferiore*: i dati nelle tabelle con ottimizzazione per la memoria devono essere contenuti nell'archiviazione OLTP in memoria associata al piano tariffario del database o disponibile nel pool elastico.</span><span class="sxs-lookup"><span data-stu-id="69e37-195">*Downgrading to a lower Premium tier*: Data in memory-optimized tables must fit within the In-Memory OLTP storage that is associated with the pricing tier of the database or is available in the elastic pool.</span></span> <span data-ttu-id="69e37-196">Se si tenta di eseguire il downgrade del piano tariffario o di spostare il database in un pool che non dispone di sufficiente spazio di archiviazione OLTP in memoria, l'operazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="69e37-196">If you try to lower the pricing tier or move the database into a pool that doesn't have enough available In-Memory OLTP storage, the operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="69e37-197">Indici Columnstore</span><span class="sxs-lookup"><span data-stu-id="69e37-197">Columnstore indexes</span></span>

<span data-ttu-id="69e37-198">*Downgrade a Basic o Standard*: gli indici columnstore sono supportati solo nel piano tariffario Premium e non nei livelli Standard o Basic.</span><span class="sxs-lookup"><span data-stu-id="69e37-198">*Downgrading to Basic or Standard*: Columnstore indexes are supported only on the Premium pricing tier, and not on the Standard or Basic tiers.</span></span> <span data-ttu-id="69e37-199">Quando si effettua il downgrade del database al piano Standard o Basic, l'indice columnstore non è più disponibile.</span><span class="sxs-lookup"><span data-stu-id="69e37-199">When you downgrade your database to Standard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="69e37-200">Il sistema conserva l'indice columnstore, ma non lo usa mai.</span><span class="sxs-lookup"><span data-stu-id="69e37-200">The system maintains your columnstore index, but it never leverages the index.</span></span> <span data-ttu-id="69e37-201">Se in seguito si torna al piano Premium, l'indice columnstore torna subito disponibile all'uso.</span><span class="sxs-lookup"><span data-stu-id="69e37-201">If you later upgrade back to Premium, your columnstore index is immediately ready to be leveraged again.</span></span>

<span data-ttu-id="69e37-202">Se dispone di un indice columnstore **cluster**, l'intera tabella non sarà più disponibile dopo il downgrade del livello.</span><span class="sxs-lookup"><span data-stu-id="69e37-202">If you have a **clustered** columnstore index, the whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="69e37-203">Pertanto è consigliabile eliminare tutti gli indici columnstore *cluster* prima di effettuare il downgrade del database al di sotto del livello Premium.</span><span class="sxs-lookup"><span data-stu-id="69e37-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below the Premium tier.</span></span>

<span data-ttu-id="69e37-204">*Downgrade a un livello Premium inferiore*: il downgrade avrà esito positivo se l'intero database rientra nelle dimensioni massime dei database relative al piano tariffario di destinazione o all'archiviazione disponibile nel pool elastico.</span><span class="sxs-lookup"><span data-stu-id="69e37-204">*Downgrading to a lower Premium tier*: This downgrade succeeds if the whole database fits within the maximum database size for the target pricing tier, or within the available storage in the elastic pool.</span></span> <span data-ttu-id="69e37-205">Non è previsto alcun impatto specifico dagli indici columnstore.</span><span class="sxs-lookup"><span data-stu-id="69e37-205">There is no specific impact from the columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-the-in-memory-oltp-sample"></a><span data-ttu-id="69e37-206">1. Installare l'esempio di OLTP in memoria</span><span class="sxs-lookup"><span data-stu-id="69e37-206">1. Install the In-Memory OLTP sample</span></span>

<span data-ttu-id="69e37-207">È possibile creare il database AdventureWorksLT di esempio con pochi clic nel [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="69e37-207">You can create the AdventureWorksLT sample database with a few clicks in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="69e37-208">I passaggi descritti in questa sezione illustrano come migliorare il database AdventureWorksLT con oggetti OLTP in memoria e dimostra i vantaggi sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="69e37-208">Then, the steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="69e37-209">Per una dimostrazione più semplice e visivamente più interessante sulle prestazioni di OLTP in memoria, vedere:</span><span class="sxs-lookup"><span data-stu-id="69e37-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="69e37-210">Versione: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="69e37-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="69e37-211">Codice sorgente: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="69e37-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="69e37-212">Procedura di installazione</span><span class="sxs-lookup"><span data-stu-id="69e37-212">Installation steps</span></span>

1. <span data-ttu-id="69e37-213">Nel [portale di Azure](https://portal.azure.com/)creare un database Premium in un server.</span><span class="sxs-lookup"><span data-stu-id="69e37-213">In the [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="69e37-214">Impostare **Origine** sul database AdventureWorksLT di esempio.</span><span class="sxs-lookup"><span data-stu-id="69e37-214">Set the **Source** to the AdventureWorksLT sample database.</span></span> <span data-ttu-id="69e37-215">Per istruzioni dettagliate, vedere [Creare il primo database SQL di Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="69e37-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="69e37-216">Connettersi al database con SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="69e37-216">Connect to the database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="69e37-217">Copiare lo [script Transact-SQL OLTP in memoria](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="69e37-217">Copy the [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) to your clipboard.</span></span> <span data-ttu-id="69e37-218">Lo script T-SQL crea gli oggetti in memoria necessari nel database AdventureWorksLT di esempio creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="69e37-218">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="69e37-219">Incollare lo script T-SQL in SSMS.exe, quindi eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="69e37-219">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="69e37-220">La clausola `MEMORY_OPTIMIZED = ON` è fondamentale nelle istruzioni CREATE TABLE,</span><span class="sxs-lookup"><span data-stu-id="69e37-220">The `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="69e37-221">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="69e37-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="69e37-222">Errore 40536</span><span class="sxs-lookup"><span data-stu-id="69e37-222">Error 40536</span></span>


<span data-ttu-id="69e37-223">Se viene visualizzato l'errore 40536 quando si esegue lo script T-SQL, verificare se il database supporta le funzionalità in memoria eseguendo questo script T-SQL:</span><span class="sxs-lookup"><span data-stu-id="69e37-223">If you get error 40536 when you run the T-SQL script, run the following T-SQL script to verify whether the database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="69e37-224">Se il risultato è **0**, le funzionalità in memoria non sono supportate, mentre **1** indica che sono supportate.</span><span class="sxs-lookup"><span data-stu-id="69e37-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="69e37-225">Per diagnosticare il problema, verificare che il livello di servizio del database sia Premium.</span><span class="sxs-lookup"><span data-stu-id="69e37-225">To diagnose the problem, ensure that the database is at the Premium service tier.</span></span>


#### <a name="about-the-created-memory-optimized-items"></a><span data-ttu-id="69e37-226">Informazioni sugli elementi creati con ottimizzazione per la memoria</span><span class="sxs-lookup"><span data-stu-id="69e37-226">About the created memory-optimized items</span></span>

<span data-ttu-id="69e37-227">**Tabelle**: l'esempio contiene le tabelle con ottimizzazione per la memoria seguenti.</span><span class="sxs-lookup"><span data-stu-id="69e37-227">**Tables**: The sample contains the following memory-optimized tables:</span></span>

- <span data-ttu-id="69e37-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="69e37-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="69e37-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="69e37-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="69e37-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="69e37-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="69e37-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="69e37-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="69e37-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="69e37-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="69e37-233">È possibile esaminare le tabelle con ottimizzazione per la memoria tramite **Esplora oggetti** in SSMS.</span><span class="sxs-lookup"><span data-stu-id="69e37-233">You can inspect memory-optimized tables through the **Object Explorer** in SSMS.</span></span> <span data-ttu-id="69e37-234">Fare doppio clic su **Tabelle** > **Filtro** > **Impostazioni filtro** > **Con ottimizzazione per la memoria**.</span><span class="sxs-lookup"><span data-stu-id="69e37-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="69e37-235">Il valore è uguale a 1.</span><span class="sxs-lookup"><span data-stu-id="69e37-235">The value equals 1.</span></span>


<span data-ttu-id="69e37-236">In alternativa, è possibile eseguire una query delle viste del catalogo, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="69e37-236">Or you can query the catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="69e37-237">**Stored procedure compilata in modo nativo**: è possibile esaminare SalesLT.usp_InsertSalesOrder_inmem usando una query delle viste del catalogo.</span><span class="sxs-lookup"><span data-stu-id="69e37-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-the-sample-oltp-workload"></a><span data-ttu-id="69e37-238">Eseguire il carico di lavoro OLTP di esempio</span><span class="sxs-lookup"><span data-stu-id="69e37-238">Run the sample OLTP workload</span></span>

<span data-ttu-id="69e37-239">L'unica differenza tra le due *stored procedure* seguenti è che la prima usa versioni con ottimizzazione per la memoria delle tabelle, mentre la seconda usa tabelle basate su disco tradizionali:</span><span class="sxs-lookup"><span data-stu-id="69e37-239">The only difference between the following two *stored procedures* is that the first procedure uses memory-optimized versions of the tables, while the second procedure uses the regular on-disk tables:</span></span>

- <span data-ttu-id="69e37-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="69e37-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="69e37-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="69e37-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="69e37-242">Questa sezione illustra come usare l'utilità **ostress.exe** per eseguire le due stored procedure in condizioni di sovraccarico.</span><span class="sxs-lookup"><span data-stu-id="69e37-242">In this section, you see how to use the handy **ostress.exe** utility to execute the two stored procedures at stressful levels.</span></span> <span data-ttu-id="69e37-243">È possibile mettere a confronto i tempi necessari per il completamento dei due test di stress.</span><span class="sxs-lookup"><span data-stu-id="69e37-243">You can compare how long it takes for the two stress runs to finish.</span></span>


<span data-ttu-id="69e37-244">Quando si esegue ostress.exe, è consigliabile passare valori di parametri specifici a entrambe:</span><span class="sxs-lookup"><span data-stu-id="69e37-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of the following:</span></span>

- <span data-ttu-id="69e37-245">Eseguire un numero elevato di connessioni simultanee, usando -n100.</span><span class="sxs-lookup"><span data-stu-id="69e37-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="69e37-246">Ripetere ogni ciclo di connessione centinaia di volte, usando -r500.</span><span class="sxs-lookup"><span data-stu-id="69e37-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="69e37-247">È opportuno, tuttavia, iniziare con valori molto più bassi, ad esempio -n10 e -r50, per assicurarsi che tutto funzioni correttamente.</span><span class="sxs-lookup"><span data-stu-id="69e37-247">However, you might want to start with much smaller values like -n10 and -r50 to ensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="69e37-248">Script per ostress.exe</span><span class="sxs-lookup"><span data-stu-id="69e37-248">Script for ostress.exe</span></span>


<span data-ttu-id="69e37-249">Questa sezione illustra lo script T-SQL incorporato nella riga di comando ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="69e37-249">This section displays the T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="69e37-250">Lo script usa gli elementi creati dallo script T-SQL installato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="69e37-250">The script uses items that were created by the T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="69e37-251">Lo script riportato di seguito inserisce un ordine di vendita di esempio con cinque voci nelle *tabelle*con ottimizzazione per la memoria seguenti:</span><span class="sxs-lookup"><span data-stu-id="69e37-251">The following script inserts a sample sales order with five line items into the following memory-optimized *tables*:</span></span>

- <span data-ttu-id="69e37-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="69e37-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="69e37-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="69e37-253">SalesLT.SalesOrderDetail_inmem</span></span>


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


<span data-ttu-id="69e37-254">Per creare la versione *_ondisk* dello script T-SQL precedente per ostress.exe, occorre sostituire le due occorrenze della sottostringa *_inmem* con *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="69e37-254">To make the *_ondisk* version of the preceding T-SQL script for ostress.exe, you would replace both occurrences of the *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="69e37-255">Queste sostituzioni interessano i nomi delle tabelle e delle stored procedure.</span><span class="sxs-lookup"><span data-stu-id="69e37-255">These replacements affect the names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="69e37-256">Installare le utilità RML e ostress</span><span class="sxs-lookup"><span data-stu-id="69e37-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="69e37-257">È consigliabile pianificare l'esecuzione di ostress.exe su una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="69e37-257">Ideally, you would plan to run ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="69e37-258">Creare una [macchina virtuale di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) nella stessa area geografica di Azure in cui risiede il database AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="69e37-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in the same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="69e37-259">È possibile eseguire ostress.exe sul computer portatile.</span><span class="sxs-lookup"><span data-stu-id="69e37-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="69e37-260">Installare nella macchina virtuale o nell'host scelto le utilità RML (Replay Markup Language),</span><span class="sxs-lookup"><span data-stu-id="69e37-260">On the VM, or on whatever host you choose, install the Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="69e37-261">che includono ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="69e37-261">The utilities include ostress.exe.</span></span>

<span data-ttu-id="69e37-262">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="69e37-262">For more information, see:</span></span>
- <span data-ttu-id="69e37-263">La discussione su ostress.exe nell'articolo relativo ai [database di esempio per OLTP in memoria](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="69e37-263">The ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="69e37-264">[Database di esempio per OLTP in memoria](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="69e37-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="69e37-265">[Blog sull'installazione di ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="69e37-265">The [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions to AdventureWorks to Demonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-the-inmem-stress-workload-first"></a><span data-ttu-id="69e37-266">Eseguire prima di tutto il test di stress del carico di lavoro per *_inmem*</span><span class="sxs-lookup"><span data-stu-id="69e37-266">Run the *_inmem* stress workload first</span></span>


<span data-ttu-id="69e37-267">Per eseguire la riga di comando ostress.exe è possibile usare una finestra del *prompt dei comandi RML* .</span><span class="sxs-lookup"><span data-stu-id="69e37-267">You can use an *RML Cmd Prompt* window to run our ostress.exe command line.</span></span> <span data-ttu-id="69e37-268">I parametri della riga di comando indicano al comando ostress di:</span><span class="sxs-lookup"><span data-stu-id="69e37-268">The command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="69e37-269">Eseguire 100 connessioni simultaneamente (-n100).</span><span class="sxs-lookup"><span data-stu-id="69e37-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="69e37-270">Fare in modo che ogni connessione esegua lo script T-SQL 50 volte (-r50).</span><span class="sxs-lookup"><span data-stu-id="69e37-270">Have each connection run the T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="69e37-271">Per eseguire la riga di comando ostress.exe precedente:</span><span class="sxs-lookup"><span data-stu-id="69e37-271">To run the preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="69e37-272">Reimpostare il contenuto dei dati del database eseguendo questo comando in SSMS per eliminare tutti i dati inseriti da esecuzioni precedenti: </span><span class="sxs-lookup"><span data-stu-id="69e37-272">Reset the database data content by running the following command in SSMS, to delete all the data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="69e37-273">Copiare il testo della riga di comando ostress.exe precedente negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="69e37-273">Copy the text of the preceding ostress.exe command line to your clipboard.</span></span>

3. <span data-ttu-id="69e37-274">Sostituire `<placeholders>` per i parametri -S -U -P -d con i valori reali corretti.</span><span class="sxs-lookup"><span data-stu-id="69e37-274">Replace the `<placeholders>` for the parameters -S -U -P -d with the correct real values.</span></span>

4. <span data-ttu-id="69e37-275">Eseguire la riga di comando modificata in una finestra dei comandi RML.</span><span class="sxs-lookup"><span data-stu-id="69e37-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="69e37-276">Il risultato è un intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="69e37-276">Result is a duration</span></span>


<span data-ttu-id="69e37-277">Al termine, ostress.exe scrive la durata dell'esecuzione come ultima riga di output nella finestra dei comandi RML.</span><span class="sxs-lookup"><span data-stu-id="69e37-277">When ostress.exe finishes, it writes the run duration as its final line of output in the RML Cmd window.</span></span> <span data-ttu-id="69e37-278">Ad esempio, per un'esecuzione dei test più breve, durata circa 1,5 minuti:</span><span class="sxs-lookup"><span data-stu-id="69e37-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="69e37-279">Reimpostare, modificare per l'esecuzione *_ondisk* ed eseguire di nuovo il test</span><span class="sxs-lookup"><span data-stu-id="69e37-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="69e37-280">Dopo aver ottenuto il risultato dell'esecuzione *_inmem*, seguire la procedura indicata di seguito per l'esecuzione *_ondisk*:</span><span class="sxs-lookup"><span data-stu-id="69e37-280">After you have the result from the *_inmem* run, perform the following steps for the *_ondisk* run:</span></span>


1. <span data-ttu-id="69e37-281">Reimpostare il database eseguendo questo comando in SSMS per eliminare tutti i dati inseriti dall'esecuzione precedente:</span><span class="sxs-lookup"><span data-stu-id="69e37-281">Reset the database by running the following command in SSMS to delete all the data that was inserted by the previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="69e37-282">Modificare la riga di comando ostress.exe per sostituire tutte le occorrenze di *_inmem* con *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="69e37-282">Edit the ostress.exe command line to replace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="69e37-283">Eseguire ostress.exe per la seconda volta e acquisire il risultato relativo alla durata.</span><span class="sxs-lookup"><span data-stu-id="69e37-283">Rerun ostress.exe for the second time, and capture the duration result.</span></span>

4. <span data-ttu-id="69e37-284">Reimpostare nuovamente il database, per eliminare in modo responsabile una potenziale grande quantità di dati di test.</span><span class="sxs-lookup"><span data-stu-id="69e37-284">Again, reset the database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="69e37-285">Risultati previsti per il confronto</span><span class="sxs-lookup"><span data-stu-id="69e37-285">Expected comparison results</span></span>

<span data-ttu-id="69e37-286">I test delle funzionalità in memoria hanno mostrato un miglioramento delle prestazioni pari a **9 volte** per questo semplice carico di lavoro, con l'utilità ostress in esecuzione in una VM di Azure nella stessa area di Azure del database.</span><span class="sxs-lookup"><span data-stu-id="69e37-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in the same Azure region as the database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-the-in-memory-analytics-sample"></a><span data-ttu-id="69e37-287">2. Installare l'esempio di analisi in memoria</span><span class="sxs-lookup"><span data-stu-id="69e37-287">2. Install the In-Memory Analytics sample</span></span>


<span data-ttu-id="69e37-288">In questa sezione vengono messi a confronto i risultati di statistiche e IO quando si usa un indice columnstore rispetto a un indice ad albero B tradizionale.</span><span class="sxs-lookup"><span data-stu-id="69e37-288">In this section, you compare the IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="69e37-289">Per l'analisi in tempo reale in un carico di lavoro OLTP, è spesso preferibile usare un indice columnstore non cluster.</span><span class="sxs-lookup"><span data-stu-id="69e37-289">For real-time analytics on an OLTP workload, it's often best to use a nonclustered columnstore index.</span></span> <span data-ttu-id="69e37-290">Per informazioni dettagliate, vedere [Descrizione degli indici columnstore](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="69e37-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-the-columnstore-analytics-test"></a><span data-ttu-id="69e37-291">Preparare il test di analisi columnstore</span><span class="sxs-lookup"><span data-stu-id="69e37-291">Prepare the columnstore analytics test</span></span>


1. <span data-ttu-id="69e37-292">Usare il portale di Azure per creare un nuovo database AdventureWorksLT dall'esempio.</span><span class="sxs-lookup"><span data-stu-id="69e37-292">Use the Azure portal to create a fresh AdventureWorksLT database from the sample.</span></span>
 - <span data-ttu-id="69e37-293">Usare esattamente questo nome.</span><span class="sxs-lookup"><span data-stu-id="69e37-293">Use that exact name.</span></span>
 - <span data-ttu-id="69e37-294">Scegliere qualsiasi livello di servizio Premium.</span><span class="sxs-lookup"><span data-stu-id="69e37-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="69e37-295">Copiare [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="69e37-295">Copy the [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) to your clipboard.</span></span>
 - <span data-ttu-id="69e37-296">Lo script T-SQL crea gli oggetti in memoria necessari nel database AdventureWorksLT di esempio creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="69e37-296">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="69e37-297">Lo script crea la tabella delle dimensioni e due tabelle dei fatti.</span><span class="sxs-lookup"><span data-stu-id="69e37-297">The script creates the Dimension table and two fact tables.</span></span> <span data-ttu-id="69e37-298">Ogni tabella dei fatti viene popolata con 3,5 milioni di righe.</span><span class="sxs-lookup"><span data-stu-id="69e37-298">The fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="69e37-299">Il completamento dello script potrebbe richiedere 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="69e37-299">The script might take 15 minutes to complete.</span></span>

3. <span data-ttu-id="69e37-300">Incollare lo script T-SQL in SSMS.exe, quindi eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="69e37-300">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="69e37-301">La parola chiave **COLUMNSTORE** è fondamentale in una istruzione **CREATE INDEX**, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="69e37-301">The **COLUMNSTORE** keyword in the **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="69e37-302">Impostare AdventureWorksLT sul livello di compatibilità 130:</span><span class="sxs-lookup"><span data-stu-id="69e37-302">Set AdventureWorksLT to compatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="69e37-303">Il livello 130 non è direttamente correlato alle funzionalità in memoria,</span><span class="sxs-lookup"><span data-stu-id="69e37-303">Level 130 is not directly related to In-Memory features.</span></span> <span data-ttu-id="69e37-304">ma offre in genere prestazioni delle query più veloci rispetto al livello 120.</span><span class="sxs-lookup"><span data-stu-id="69e37-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="69e37-305">Tabelle e indici columnstore fondamentali</span><span class="sxs-lookup"><span data-stu-id="69e37-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="69e37-306">dbo.FactResellerSalesXL_CCI è una tabella contenente un indice *columnstore* cluster, che presenta una compressione avanzata a livello di dati.</span><span class="sxs-lookup"><span data-stu-id="69e37-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at the *data* level.</span></span>

- <span data-ttu-id="69e37-307">dbo.FactResellerSalesXL_PageCompressed è una tabella contenente un indice cluster equivalente tradizionale, che presenta una compressione solo a livello di *pagina*.</span><span class="sxs-lookup"><span data-stu-id="69e37-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at the *page* level.</span></span>


#### <a name="key-queries-to-compare-the-columnstore-index"></a><span data-ttu-id="69e37-308">Query fondamentali per il confronto dell'indice columnstore</span><span class="sxs-lookup"><span data-stu-id="69e37-308">Key queries to compare the columnstore index</span></span>


<span data-ttu-id="69e37-309">Sono disponibili [diversi tipi di query T-SQ](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) che è possibile eseguire per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="69e37-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) to see performance improvements.</span></span> <span data-ttu-id="69e37-310">Nel passaggio 2 nello script T-SQL, prestare attenzione a questa coppia di query.</span><span class="sxs-lookup"><span data-stu-id="69e37-310">In step 2 in the T-SQL script, pay attention to this pair of queries.</span></span> <span data-ttu-id="69e37-311">Le due query differiscono per una sola riga:</span><span class="sxs-lookup"><span data-stu-id="69e37-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="69e37-312">Un indice columnstore cluster si trova nella tabella FactResellerSalesXL\_CCI.</span><span class="sxs-lookup"><span data-stu-id="69e37-312">A clustered columnstore index is in the FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="69e37-313">L'estratto dallo script T-SQL riportato di seguito permette di stampare le statistiche per IO e TIME per la query di ogni tabella.</span><span class="sxs-lookup"><span data-stu-id="69e37-313">The following T-SQL script excerpt prints statistics for IO and TIME for the query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order to see Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins the Fact Table with dimension tables
-- Note this query will run on the Page Compressed table, Note down the time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is the same Prior query on a table with a clustered columnstore index CCI
-- The comparison numbers are even more dramatic the larger the table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

<span data-ttu-id="69e37-314">In un database con piano tariffario P2 è possibile raggiungere circa 9X il guadagno sulle prestazioni per la query tramite l'indice columnstore cluster rispetto a un indice tradizionale.</span><span class="sxs-lookup"><span data-stu-id="69e37-314">In a database with the P2 pricing tier, you can expect about nine times the performance gain for this query by using the clustered columnstore index compared with the traditional index.</span></span> <span data-ttu-id="69e37-315">Con P15, è possibile prevedere un miglioramento delle prestazioni pari a 57X usando l'indice columnstore.</span><span class="sxs-lookup"><span data-stu-id="69e37-315">With P15, you can expect about 57 times the performance gain by using the columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="69e37-316">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69e37-316">Next steps</span></span>

- [<span data-ttu-id="69e37-317">Avvio rapido 1: Tecnologie OLTP in memoria per ottimizzare le prestazioni di T-SQL</span><span class="sxs-lookup"><span data-stu-id="69e37-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="69e37-318">Usare OLTP in memoria in un'applicazione esistente del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="69e37-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="69e37-319">[Monitoraggio dell'archiviazione OLTP in memoria](sql-database-in-memory-oltp-monitoring.md) per OLTP in memoria.</span><span class="sxs-lookup"><span data-stu-id="69e37-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="69e37-320">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="69e37-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="69e37-321">Approfondimenti</span><span class="sxs-lookup"><span data-stu-id="69e37-321">Deeper information</span></span>

- <span data-ttu-id="69e37-322">[Informazioni in Learn how Quorum doubles key database's workload while lowering DTU by 70% with In-Memory OLTP in SQL Databas](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database) (Il quorum raddoppia il carico di lavoro del database principale riducendo il DTU del 70% con OLTP in memoria nel database SQL)</span><span class="sxs-lookup"><span data-stu-id="69e37-322">[Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>

- <span data-ttu-id="69e37-323">[In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/) (Post di blog su OLTP nel database SQL di Azure)</span><span class="sxs-lookup"><span data-stu-id="69e37-323">[In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

- [<span data-ttu-id="69e37-324">Informazioni su OLTP in memoria</span><span class="sxs-lookup"><span data-stu-id="69e37-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="69e37-325">Informazioni sugli indici columnstore</span><span class="sxs-lookup"><span data-stu-id="69e37-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="69e37-326">Informazioni sulle analisi operative in tempo reale</span><span class="sxs-lookup"><span data-stu-id="69e37-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="69e37-327">Vedere l'articolo sui [modelli comuni dei carichi di lavoro e considerazioni relative alla migrazione](http://msdn.microsoft.com/library/dn673538.aspx), che descrive modelli di carico di lavoro in cui OLTP in memoria fornisce in genere miglioramenti significativi delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="69e37-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="69e37-328">Progettazione di applicazioni</span><span class="sxs-lookup"><span data-stu-id="69e37-328">Application design</span></span>

- [<span data-ttu-id="69e37-329">OLTP in memoria (ottimizzazione in memoria)</span><span class="sxs-lookup"><span data-stu-id="69e37-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="69e37-330">Usare OLTP in memoria in un'applicazione esistente del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="69e37-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="69e37-331">Strumenti</span><span class="sxs-lookup"><span data-stu-id="69e37-331">Tools</span></span>

- [<span data-ttu-id="69e37-332">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="69e37-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="69e37-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="69e37-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="69e37-334">SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="69e37-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
