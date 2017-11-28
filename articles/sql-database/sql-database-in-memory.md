---
title: tecnologie di Database SQL In memoria aaaAzure | Documenti Microsoft
description: Tecnologie In memoria del Database SQL Azure migliorare notevolmente le prestazioni di hello delle transazioni e i carichi di lavoro analitica. Informazioni su come tootake sfruttare tali tecnologie.
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
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="9ed90-104">Ottimizzare le prestazioni tramite le tecnologie in memoria nel database SQL</span><span class="sxs-lookup"><span data-stu-id="9ed90-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="9ed90-105">Tramite le tecnologie in memoria del database SQL di Azure, è possibile migliorare le prestazioni di diversi carichi di lavoro: transazionale (elaborazione transazionale online o OLTP), analitica (elaborazione analitica online o OLAP) e mista (elaborazione ibrida transazione/analitica o HTAP).</span><span class="sxs-lookup"><span data-stu-id="9ed90-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="9ed90-106">A causa di hello query più efficienti e l'elaborazione delle transazioni, le tecnologie In memoria consentono anche di costo tooreduce.</span><span class="sxs-lookup"><span data-stu-id="9ed90-106">Because of hello more efficient query and transaction processing, In-Memory technologies also help you tooreduce cost.</span></span> <span data-ttu-id="9ed90-107">In genere non occorre hello tooupgrade tariffario hello database tooachieve dei miglioramenti delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9ed90-107">You typically don't need tooupgrade hello pricing tier of hello database tooachieve performance gains.</span></span> <span data-ttu-id="9ed90-108">In alcuni casi, potrebbe anche essere possibile ridurre hello tariffario, mentre ancora osservare i miglioramenti delle prestazioni con le tecnologie In memoria.</span><span class="sxs-lookup"><span data-stu-id="9ed90-108">In some cases, you might even be able reduce hello pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="9ed90-109">Di seguito sono riportati due esempi di come OLTP In memoria consentito toosignificantly migliorare le prestazioni:</span><span class="sxs-lookup"><span data-stu-id="9ed90-109">Here are two examples of how In-Memory OLTP helped toosignificantly improve performance:</span></span>

- <span data-ttu-id="9ed90-110">Con OLTP In memoria, [Quorum soluzioni di Business è stato in grado di toodouble relativo carico di lavoro migliorando Dtu del 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="9ed90-110">By using In-Memory OLTP, [Quorum Business Solutions was able toodouble their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="9ed90-111">DTU significa *unità di velocità effettiva database* e include una misurazione del consumo di risorse.</span><span class="sxs-lookup"><span data-stu-id="9ed90-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="9ed90-112">Hello video seguente viene illustrato un miglioramento significativo del consumo di risorse con un carico di lavoro di esempio: [OLTP In memoria in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span><span class="sxs-lookup"><span data-stu-id="9ed90-112">hello following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="9ed90-113">Per ulteriori informazioni, vedere hello post di blog: [OLTP In memoria in cui il Post di Blog di Azure SQL Database](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="9ed90-113">For more details, see hello blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="9ed90-114">Tecnologie in memoria sono disponibili in tutti i database nel livello Premium hello, inclusi i database nel pool elastico Premium.</span><span class="sxs-lookup"><span data-stu-id="9ed90-114">In-Memory technologies are available in all databases in hello Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="9ed90-115">Hello video seguente viene illustrato potenziali miglioramenti delle prestazioni con le tecnologie In memoria nel Database di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed90-115">hello following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="9ed90-116">Tenere presente che miglioramento delle prestazioni di hello che viene visualizzato sempre dipende da molti fattori, tra cui natura hello del carico di lavoro di hello e dati, il criterio di accesso del database di hello e così via.</span><span class="sxs-lookup"><span data-stu-id="9ed90-116">Remember that hello performance gain that you see always depends on many factors, including hello nature of hello workload and data, access pattern of hello database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="9ed90-117">Database SQL di Azure è hello seguenti tecnologie In memoria:</span><span class="sxs-lookup"><span data-stu-id="9ed90-117">Azure SQL Database has hello following In-Memory technologies:</span></span>

- <span data-ttu-id="9ed90-118">*OLTP in memoria*: aumenta la velocità effettiva e riduce la latenza per l'elaborazione delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="9ed90-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="9ed90-119">Gli scenari che beneficiano dell'OLTP in memoria sono: elaborazione transazionale ad alta velocità di elaborazione, come l'inserimento di dati commerciali e da videogiochi, da eventi o dispositivi IoT, il caching, il caricamento di dati, le tabelle temporanee e gli scenari con variabili di tabella.</span><span class="sxs-lookup"><span data-stu-id="9ed90-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="9ed90-120">*Indici columnstore cluster* ridurre il footprint di memoria (i tempi di too10) e migliorare le prestazioni per le query di creazione di report e analitica.</span><span class="sxs-lookup"><span data-stu-id="9ed90-120">*Clustered columnstore indexes* reduce your storage footprint (up too10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="9ed90-121">È possibile utilizzarlo con le tabelle dei fatti in toofit di data mart i dati più dati nel database e migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9ed90-121">You can use it with fact tables in your data marts toofit more data in your database and improve performance.</span></span> <span data-ttu-id="9ed90-122">Inoltre, è possibile utilizzarlo con i dati cronologici in tooarchive il database operativo ed essere in grado di tooquery too10 ore di più dati.</span><span class="sxs-lookup"><span data-stu-id="9ed90-122">Also, you can use it with historical data in your operational database tooarchive and be able tooquery up too10 times more data.</span></span>
- <span data-ttu-id="9ed90-123">*Indici columnstore non cluster* per help HTAP si toogain approfondite in tempo reale dell'azienda tramite l'esecuzione di query hello operational database direttamente, senza hello necessità toorun un'estrazione dispendiosa, trasformazione e il processo di caricamento (ETL) e in attesa per hello dati warehouse toobe popolato.</span><span class="sxs-lookup"><span data-stu-id="9ed90-123">*Nonclustered columnstore indexes* for HTAP help you toogain real-time insights into your business through querying hello operational database directly, without hello need toorun an expensive extract, transform, and load (ETL) process and wait for hello data warehouse toobe populated.</span></span> <span data-ttu-id="9ed90-124">Indici columnstore non cluster consentono l'esecuzione molto rapida delle query analitica nel database OLTP di hello, riducendo l'impatto di hello sul carico di lavoro operativo hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on hello OLTP database, while reducing hello impact on hello operational workload.</span></span>
- <span data-ttu-id="9ed90-125">È anche possibile combinazione di hello di una tabella con ottimizzazione per la memoria con un indice columnstore.</span><span class="sxs-lookup"><span data-stu-id="9ed90-125">You can also have hello combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="9ed90-126">Questa combinazione consente tooperform molto rapida elaborazione delle transazioni e troppo*contemporaneamente* fase analitica esegue una query molto rapidamente sul hello stessi dati.</span><span class="sxs-lookup"><span data-stu-id="9ed90-126">This combination enables you tooperform very fast transaction processing, and too*concurrently* run analytics queries very quickly on hello same data.</span></span>

<span data-ttu-id="9ed90-127">Sia gli indici columnstore e OLTP In memoria sono stati parte del prodotto SQL Server hello sin 2012 e 2014, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="9ed90-127">Both columnstore indexes and In-Memory OLTP have been part of hello SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="9ed90-128">Database SQL di Azure e SQL Server condividono hello stessa implementazione delle tecnologie In memoria.</span><span class="sxs-lookup"><span data-stu-id="9ed90-128">Azure SQL Database and SQL Server share hello same implementation of In-Memory technologies.</span></span> <span data-ttu-id="9ed90-129">In futuro, le nuove funzionalità per queste tecnologie verranno integrate prima nel database SQL di Azure e poi in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9ed90-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="9ed90-130">In questo argomento vengono descritti gli aspetti di OLTP In memoria e columnstore indici tooAzure specifico Database SQL e vengono forniti esempi di:</span><span class="sxs-lookup"><span data-stu-id="9ed90-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific tooAzure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="9ed90-131">Si noterà impatto hello di queste tecnologie, sui limiti di dimensioni di archiviazione e i dati.</span><span class="sxs-lookup"><span data-stu-id="9ed90-131">You'll see hello impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="9ed90-132">Verrà visualizzato come toomanage hello lo spostamento di database che utilizzano queste tecnologie tra hello livelli di prezzo diverso.</span><span class="sxs-lookup"><span data-stu-id="9ed90-132">You'll see how toomanage hello movement of databases that use these technologies between hello different pricing tiers.</span></span>
- <span data-ttu-id="9ed90-133">Si noterà due esempi che illustrano l'utilizzo di hello di OLTP In memoria, nonché gli indici columnstore in Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed90-133">You'll see two samples that illustrate hello use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="9ed90-134">Hello seguenti risorse per ulteriori informazioni, vedere.</span><span class="sxs-lookup"><span data-stu-id="9ed90-134">See hello following resources for more information.</span></span>

<span data-ttu-id="9ed90-135">Informazioni dettagliate sulle tecnologie di hello:</span><span class="sxs-lookup"><span data-stu-id="9ed90-135">In-depth information about hello technologies:</span></span>

- <span data-ttu-id="9ed90-136">[Panoramica di OLTP in memoria e scenari di utilizzo](https://msdn.microsoft.com/library/mt774593.aspx) (include riferimenti toocustomer case study e informazioni tooget avviato)</span><span class="sxs-lookup"><span data-stu-id="9ed90-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references toocustomer case studies and information tooget started)</span></span>
- [<span data-ttu-id="9ed90-137">OLTP in memoria</span><span class="sxs-lookup"><span data-stu-id="9ed90-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="9ed90-138">Descrizione degli indici columnstore</span><span class="sxs-lookup"><span data-stu-id="9ed90-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="9ed90-139">L'elaborazione analitica e transazionale ibrida (HTAP), anche nota come [analisi operativa in tempo reale](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="9ed90-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="9ed90-140">Riportata una breve spiegazione su OLTP In memoria: [avvio rapido 1: tecnologie OLTP In memoria per più rapidamente le prestazioni di T-SQL](http://msdn.microsoft.com/library/mt694156.aspx) (un altro articolo toohelp iniziare)</span><span class="sxs-lookup"><span data-stu-id="9ed90-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article toohelp you get started)</span></span>

<span data-ttu-id="9ed90-141">Video dettagliate sulle tecnologie di hello:</span><span class="sxs-lookup"><span data-stu-id="9ed90-141">In-depth videos about hello technologies:</span></span>

- <span data-ttu-id="9ed90-142">[OLTP in memoria nel Database di SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (che contiene una dimostrazione delle prestazioni vantaggi e i passaggi tooreproduce questi risultati manualmente)</span><span class="sxs-lookup"><span data-stu-id="9ed90-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps tooreproduce these results yourself)</span></span>
- [<span data-ttu-id="9ed90-143">Video OLTP in memoria: Che cos'è e quando e come toouse,</span><span class="sxs-lookup"><span data-stu-id="9ed90-143">In-Memory OLTP Videos: What it is and When/How toouse it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="9ed90-144">Indice ColumnStore: Video sull'analisi in memoria da Ignite 2016</span><span class="sxs-lookup"><span data-stu-id="9ed90-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="9ed90-145">Dimensioni di archiviazione e dati</span><span class="sxs-lookup"><span data-stu-id="9ed90-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="9ed90-146">Limite su dimensioni dei dati e archiviazione per OLTP in memoria</span><span class="sxs-lookup"><span data-stu-id="9ed90-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="9ed90-147">OLTP in memoria include tabelle con ottimizzazione per la memoria, che vengono usate per archiviare i dati utente.</span><span class="sxs-lookup"><span data-stu-id="9ed90-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="9ed90-148">Queste tabelle sono necessarie toofit in memoria.</span><span class="sxs-lookup"><span data-stu-id="9ed90-148">These tables are required toofit in memory.</span></span> <span data-ttu-id="9ed90-149">Perché vengono gestiti memoria direttamente nel servizio di Database SQL di hello, abbiamo concetto hello di una quota per i dati utente.</span><span class="sxs-lookup"><span data-stu-id="9ed90-149">Because you manage memory directly in hello SQL Database service, we have hello  concept of a quota for user data.</span></span> <span data-ttu-id="9ed90-150">Questo concetto è noto tooas *archiviazione OLTP In memoria*.</span><span class="sxs-lookup"><span data-stu-id="9ed90-150">This idea is referred tooas *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="9ed90-151">Ogni piano tariffario relativo a database autonomi e pool elastici supportati include una certa quantità di spazio di archiviazione OLTP in memoria.</span><span class="sxs-lookup"><span data-stu-id="9ed90-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="9ed90-152">In fase di hello di scrittura, si ottiene un gigabyte di spazio di archiviazione per ogni unità di transazione database (Dtu) 125 o di un database elastico (Edtu) di unità di transazione.</span><span class="sxs-lookup"><span data-stu-id="9ed90-152">At hello time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="9ed90-153">Hello [livelli di servizio di Database SQL](sql-database-service-tiers.md) articolo ha elenco ufficiale di hello hello OLTP In memoria di archiviazione di disponibili per ogni database autonomo e il pool elastico piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="9ed90-153">hello [SQL Database service tiers](sql-database-service-tiers.md) article has hello official list of hello In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="9ed90-154">Hello dopo il numero di elementi verso l'estremità di archiviazione di OLTP In memoria:</span><span class="sxs-lookup"><span data-stu-id="9ed90-154">hello following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="9ed90-155">Righe di dati utente attive nelle tabelle con ottimizzazione per la memoria e variabili di tabella.</span><span class="sxs-lookup"><span data-stu-id="9ed90-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="9ed90-156">Si noti che le versioni precedenti di riga non conteggiati per cap hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-156">Note that old row versions don't count toward hello cap.</span></span>
- <span data-ttu-id="9ed90-157">Indici nelle tabelle con ottimizzazione per la memoria.</span><span class="sxs-lookup"><span data-stu-id="9ed90-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="9ed90-158">Costi operativi delle operazioni ALTER TABLE.</span><span class="sxs-lookup"><span data-stu-id="9ed90-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="9ed90-159">Se si raggiunge il limite di hello, viene visualizzato un errore di quota di uscita e, non sarà più in grado di tooinsert o aggiornamento di dati.</span><span class="sxs-lookup"><span data-stu-id="9ed90-159">If you hit hello cap, you receive an out-of-quota error, and you are no longer able tooinsert or update data.</span></span> <span data-ttu-id="9ed90-160">toomitigate questo errore, eliminare i dati o aumentare hello a livello di database hello o un pool di prezzo.</span><span class="sxs-lookup"><span data-stu-id="9ed90-160">toomitigate this error, delete data or increase hello pricing tier of hello database or pool.</span></span>

<span data-ttu-id="9ed90-161">Per informazioni dettagliate sul monitoraggio di utilizzo di spazio di archiviazione di OLTP In memoria e la configurazione degli avvisi quando quasi raggiunto limite massimo di hello, vedere [archiviazione di monitoraggio In memoria](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="9ed90-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit hello cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="9ed90-162">Informazioni sui pool elastici</span><span class="sxs-lookup"><span data-stu-id="9ed90-162">About elastic pools</span></span>

<span data-ttu-id="9ed90-163">Il pool elastico, hello archiviazione OLTP In memoria è condivisa tra tutti i database nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-163">With elastic pools, hello In-Memory OLTP storage is shared across all databases in hello pool.</span></span> <span data-ttu-id="9ed90-164">Pertanto, utilizzo di hello in un database può influire altri database.</span><span class="sxs-lookup"><span data-stu-id="9ed90-164">Therefore, hello usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="9ed90-165">Esistono due metodi per la risoluzione di questo problema:</span><span class="sxs-lookup"><span data-stu-id="9ed90-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="9ed90-166">Consente di configurare un numero massimo-eDTU per database che è inferiore al numero di eDTU hello per il pool di hello nel suo complesso.</span><span class="sxs-lookup"><span data-stu-id="9ed90-166">Configure a Max-eDTU for databases that is lower than hello eDTU count for hello pool as a whole.</span></span> <span data-ttu-id="9ed90-167">Questo valore massimo per le coperture spazio di archiviazione OLTP In memoria hello, in qualsiasi database nel pool di hello, dimensioni toohello corrispondente numero di eDTU toohello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-167">This maximum caps hello In-Memory OLTP storage utilization, in any database in hello pool, toohello size that corresponds toohello eDTU count.</span></span>
- <span data-ttu-id="9ed90-168">Configurare Min-eDTU su un valore maggiore di 0.</span><span class="sxs-lookup"><span data-stu-id="9ed90-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="9ed90-169">Questo modo si garantisce che ogni database nel pool di hello quantità hello di archiviazione di OLTP In memoria disponibile corrispondente toohello minimo configurato Min eDTU.</span><span class="sxs-lookup"><span data-stu-id="9ed90-169">This minimum guarantees that each database in hello pool has hello amount of available In-Memory OLTP storage that corresponds toohello configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="9ed90-170">Dimensioni dei dati e archiviazione per gli indici columnstore</span><span class="sxs-lookup"><span data-stu-id="9ed90-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="9ed90-171">Gli indici ColumnStore non sono necessari toofit in memoria.</span><span class="sxs-lookup"><span data-stu-id="9ed90-171">Columnstore indexes aren't required toofit in memory.</span></span> <span data-ttu-id="9ed90-172">Pertanto, hello solo limite dimensione hello degli indici hello è hello dimensione massima complessiva del database, che è documentato in hello [livelli di servizio di Database SQL](sql-database-service-tiers.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="9ed90-172">Therefore, hello only cap on hello size of hello indexes is hello maximum overall database size, which is documented in hello [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="9ed90-173">Quando si utilizzano gli indici columnstore cluster, la compressione a colonne viene utilizzata per l'archiviazione di tabelle di base hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-173">When you use clustered columnstore indexes, columnar compression is used for hello base table storage.</span></span> <span data-ttu-id="9ed90-174">Questo tipo di compressione può ridurre notevolmente il footprint di memoria hello dei dati utente, il che significa che è possibile inserire più dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-174">This compression can significantly reduce hello storage footprint of your user data, which means that you can fit more data in hello database.</span></span> <span data-ttu-id="9ed90-175">E la compressione di hello può essere ulteriormente aumentata con [la compressione dell'archivio colonne](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="9ed90-175">And hello compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="9ed90-176">quantità di Hello della compressione che è possibile ottenere dipende dalla natura hello dei dati di hello, ma la compressione di 10 volte hello non è insolita.</span><span class="sxs-lookup"><span data-stu-id="9ed90-176">hello amount of compression that you can achieve depends on hello nature of hello data, but 10 times hello compression is not uncommon.</span></span>

<span data-ttu-id="9ed90-177">Ad esempio, se si dispone di un database con una dimensione massima di 1 terabyte (TB) e per ottenere la compressione di 10 volte hello utilizzare gli indici columnstore, è possibile adattare un totale di 10 TB di dati dell'utente nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times hello compression by using columnstore indexes, you can fit a total of 10 TB of user data in hello database.</span></span>

<span data-ttu-id="9ed90-178">Quando si utilizzano gli indici columnstore non cluster, tabella di base hello è ancora archiviata in formato rowstore tradizionali hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-178">When you use nonclustered columnstore indexes, hello base table is still stored in hello traditional rowstore format.</span></span> <span data-ttu-id="9ed90-179">Pertanto, hello risparmi di archiviazione non sono grandi come con gli indici columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="9ed90-179">Therefore, hello storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="9ed90-180">Tuttavia, se si desidera sostituire un numero di indici non cluster tradizionale con un indice columnstore singolo, è possibile visualizzare ancora un risparmio in footprint di memoria hello per tabella hello complessivo.</span><span class="sxs-lookup"><span data-stu-id="9ed90-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in hello storage footprint for hello table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="9ed90-181">Spostamento dei database tra i piani tariffari tramite tecnologie in memoria</span><span class="sxs-lookup"><span data-stu-id="9ed90-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="9ed90-182">Esistono mai eventuali incompatibilità o altri problemi quando si esegue l'aggiornamento tooa superiore tariffario, ad esempio da tooPremium Standard.</span><span class="sxs-lookup"><span data-stu-id="9ed90-182">There are never any incompatibilities or other problems when you upgrade tooa higher pricing tier, such as from Standard tooPremium.</span></span> <span data-ttu-id="9ed90-183">risorse e funzionalità disponibili hello solo aumentano.</span><span class="sxs-lookup"><span data-stu-id="9ed90-183">hello available functionality and resources only increase.</span></span>

<span data-ttu-id="9ed90-184">Ma hello downgrade tariffario può influire negativamente del database.</span><span class="sxs-lookup"><span data-stu-id="9ed90-184">But downgrading hello pricing tier can negatively impact your database.</span></span> <span data-ttu-id="9ed90-185">impatto di Hello è particolarmente evidente quando esegue il downgrade da Premium tooStandard o di base per il database contiene oggetti di OLTP In memoria.</span><span class="sxs-lookup"><span data-stu-id="9ed90-185">hello impact is especially apparent when you downgrade from Premium tooStandard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="9ed90-186">Le tabelle con ottimizzazione per la memoria e gli indici columnstore, sono disponibili dopo il downgrade di hello (anche se rimangono visibili).</span><span class="sxs-lookup"><span data-stu-id="9ed90-186">Memory-optimized tables, and columnstore indexes, are unavailable after hello downgrade (even if they remain visible).</span></span> <span data-ttu-id="9ed90-187">Hello stesse considerazioni si applicano quando si sta riducendo hello a livello di un pool elastico di prezzo o spostamento di un database con le tecnologie In memoria, in uno Standard o Basic pool elastico.</span><span class="sxs-lookup"><span data-stu-id="9ed90-187">hello same considerations apply when you're lowering hello pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="9ed90-188">OLTP in memoria</span><span class="sxs-lookup"><span data-stu-id="9ed90-188">In-Memory OLTP</span></span>

<span data-ttu-id="9ed90-189">*Downgrade tooBasic/Standard*: OLTP In memoria non è supportato nei database di livello Standard o Basic hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-189">*Downgrading tooBasic/Standard*: In-Memory OLTP isn't supported in databases in hello Standard or Basic tier.</span></span> <span data-ttu-id="9ed90-190">Inoltre, non è possibile toomove un database che include qualsiasi toohello oggetti OLTP In memoria livello Standard o Basic.</span><span class="sxs-lookup"><span data-stu-id="9ed90-190">In addition, it isn't possible toomove a database that has any In-Memory OLTP objects toohello Standard or Basic tier.</span></span>

<span data-ttu-id="9ed90-191">Prima effettuare il downgrade hello database tooStandard/Basic, rimuovere tutte le tabelle con ottimizzazione per la memoria e i tipi di tabella, nonché tutti i moduli T-SQL compilati in modo nativo.</span><span class="sxs-lookup"><span data-stu-id="9ed90-191">Before you downgrade hello database tooStandard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="9ed90-192">Se un determinato database supporta OLTP In memoria è toounderstand un livello di codice.</span><span class="sxs-lookup"><span data-stu-id="9ed90-192">There is a programmatic way toounderstand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="9ed90-193">È possibile eseguire hello query Transact-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="9ed90-193">You can execute hello following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="9ed90-194">Se la query hello restituisce **1**, OLTP In memoria è supportato in questo database.</span><span class="sxs-lookup"><span data-stu-id="9ed90-194">If hello query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="9ed90-195">*Il downgrade di livello Premium inferiore tooa*: dati nelle tabelle con ottimizzazione per la memoria devono essere contenuta in archiviazione di OLTP In memoria hello che è associato a hello piano tariffario del database hello o nel pool elastico hello è disponibile.</span><span class="sxs-lookup"><span data-stu-id="9ed90-195">*Downgrading tooa lower Premium tier*: Data in memory-optimized tables must fit within hello In-Memory OLTP storage that is associated with hello pricing tier of hello database or is available in hello elastic pool.</span></span> <span data-ttu-id="9ed90-196">Se si tenta di hello toolower livello di prezzo o spostare database hello in un pool che non dispone di sufficiente spazio di archiviazione di OLTP In memoria disponibile, hello operazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="9ed90-196">If you try toolower hello pricing tier or move hello database into a pool that doesn't have enough available In-Memory OLTP storage, hello operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="9ed90-197">Indici Columnstore</span><span class="sxs-lookup"><span data-stu-id="9ed90-197">Columnstore indexes</span></span>

<span data-ttu-id="9ed90-198">*Downgrade Standard o tooBasic*: gli indici sono supportati solo nel piano tariffario Premium hello e non in Columnstore hello livelli Standard o Basic.</span><span class="sxs-lookup"><span data-stu-id="9ed90-198">*Downgrading tooBasic or Standard*: Columnstore indexes are supported only on hello Premium pricing tier, and not on hello Standard or Basic tiers.</span></span> <span data-ttu-id="9ed90-199">Quando si esegue il downgrade del database tooStandard o Basic, l'indice columnstore non è più disponibile.</span><span class="sxs-lookup"><span data-stu-id="9ed90-199">When you downgrade your database tooStandard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="9ed90-200">sistema di Hello mantiene l'indice columnstore, ma mai sfrutta indice hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-200">hello system maintains your columnstore index, but it never leverages hello index.</span></span> <span data-ttu-id="9ed90-201">Se si aggiorna in un secondo momento tooPremium indietro, l'indice columnstore è immediatamente pronto toobe utilizzati nuovamente.</span><span class="sxs-lookup"><span data-stu-id="9ed90-201">If you later upgrade back tooPremium, your columnstore index is immediately ready toobe leveraged again.</span></span>

<span data-ttu-id="9ed90-202">Se dispone di un **cluster** indice columnstore, intera tabella hello diventa disponibile dopo il downgrade di livello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-202">If you have a **clustered** columnstore index, hello whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="9ed90-203">Pertanto è consigliabile eliminare tutti *cluster* di indici columnstore prima effettuare il downgrade del database di sotto di livello Premium hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below hello Premium tier.</span></span>

<span data-ttu-id="9ed90-204">*Il downgrade di livello Premium inferiore tooa*: questa operazione ha esito positivo se l'intero database hello rientra nelle dimensioni massime del database hello per destinazione hello livello di prezzo o all'interno dell'archiviazione disponibile nel pool elastico hello hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-204">*Downgrading tooa lower Premium tier*: This downgrade succeeds if hello whole database fits within hello maximum database size for hello target pricing tier, or within hello available storage in hello elastic pool.</span></span> <span data-ttu-id="9ed90-205">Non ha alcun impatto determinato dagli indici columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-205">There is no specific impact from hello columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a><span data-ttu-id="9ed90-206">1. Installare l'esempio di OLTP In memoria hello</span><span class="sxs-lookup"><span data-stu-id="9ed90-206">1. Install hello In-Memory OLTP sample</span></span>

<span data-ttu-id="9ed90-207">È possibile creare il database di esempio AdventureWorksLT hello con pochi clic nel hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9ed90-207">You can create hello AdventureWorksLT sample database with a few clicks in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="9ed90-208">Quindi, hello passaggi in questa sezione illustrano come è possibile arricchire il database AdventureWorksLT con gli oggetti di OLTP In memoria e illustrano i vantaggi delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9ed90-208">Then, hello steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="9ed90-209">Per una dimostrazione più semplice e visivamente più interessante sulle prestazioni di OLTP in memoria, vedere:</span><span class="sxs-lookup"><span data-stu-id="9ed90-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="9ed90-210">Versione: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="9ed90-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="9ed90-211">Codice sorgente: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="9ed90-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="9ed90-212">Procedura di installazione</span><span class="sxs-lookup"><span data-stu-id="9ed90-212">Installation steps</span></span>

1. <span data-ttu-id="9ed90-213">In hello [portale di Azure](https://portal.azure.com/), creare un database Premium in un server.</span><span class="sxs-lookup"><span data-stu-id="9ed90-213">In hello [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="9ed90-214">Set hello **origine** toohello database di esempio AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="9ed90-214">Set hello **Source** toohello AdventureWorksLT sample database.</span></span> <span data-ttu-id="9ed90-215">Per istruzioni dettagliate, vedere [Creare il primo database SQL di Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9ed90-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="9ed90-216">La connessione a database toohello con SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed90-216">Connect toohello database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="9ed90-217">Hello copia [script Transact-SQL di In-Memory OLTP](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour Appunti.</span><span class="sxs-lookup"><span data-stu-id="9ed90-217">Copy hello [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour clipboard.</span></span> <span data-ttu-id="9ed90-218">Hello script T-SQL hello crea oggetti In memoria necessarie nel database di esempio AdventureWorksLT hello creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="9ed90-218">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="9ed90-219">Incollare lo script T-SQL di hello in SQL Server Management Studio e quindi eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-219">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="9ed90-220">Hello `MEMORY_OPTIMIZED = ON` istruzioni CREATE TABLE sono fondamentali.</span><span class="sxs-lookup"><span data-stu-id="9ed90-220">hello `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="9ed90-221">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9ed90-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="9ed90-222">Errore 40536</span><span class="sxs-lookup"><span data-stu-id="9ed90-222">Error 40536</span></span>


<span data-ttu-id="9ed90-223">Se viene visualizzato l'errore 40536 quando si esegue script hello T-SQL, eseguire hello seguente tooverify script T-SQL se il database di hello supporta In memoria:</span><span class="sxs-lookup"><span data-stu-id="9ed90-223">If you get error 40536 when you run hello T-SQL script, run hello following T-SQL script tooverify whether hello database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="9ed90-224">Se il risultato è **0**, le funzionalità in memoria non sono supportate, mentre **1** indica che sono supportate.</span><span class="sxs-lookup"><span data-stu-id="9ed90-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="9ed90-225">problema di hello toodiagnose, assicurarsi che il database hello sia a livello di servizio Premium hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-225">toodiagnose hello problem, ensure that hello database is at hello Premium service tier.</span></span>


#### <a name="about-hello-created-memory-optimized-items"></a><span data-ttu-id="9ed90-226">Sui hello creata articoli con ottimizzazione per la memoria</span><span class="sxs-lookup"><span data-stu-id="9ed90-226">About hello created memory-optimized items</span></span>

<span data-ttu-id="9ed90-227">**Tabelle**: esempio hello contiene hello le tabelle con ottimizzazione per la memoria seguenti:</span><span class="sxs-lookup"><span data-stu-id="9ed90-227">**Tables**: hello sample contains hello following memory-optimized tables:</span></span>

- <span data-ttu-id="9ed90-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="9ed90-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="9ed90-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="9ed90-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="9ed90-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="9ed90-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="9ed90-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="9ed90-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="9ed90-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="9ed90-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="9ed90-233">È possibile esaminare le tabelle con ottimizzazione per la memoria tramite hello **Esplora oggetti** in SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="9ed90-233">You can inspect memory-optimized tables through hello **Object Explorer** in SSMS.</span></span> <span data-ttu-id="9ed90-234">Fare doppio clic su **Tabelle** > **Filtro** > **Impostazioni filtro** > **Con ottimizzazione per la memoria**.</span><span class="sxs-lookup"><span data-stu-id="9ed90-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="9ed90-235">il valore di Hello è uguale a 1.</span><span class="sxs-lookup"><span data-stu-id="9ed90-235">hello value equals 1.</span></span>


<span data-ttu-id="9ed90-236">In alternativa, è possibile eseguire query viste del catalogo hello, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9ed90-236">Or you can query hello catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="9ed90-237">**Stored procedure compilata in modo nativo**: è possibile esaminare SalesLT.usp_InsertSalesOrder_inmem usando una query delle viste del catalogo.</span><span class="sxs-lookup"><span data-stu-id="9ed90-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a><span data-ttu-id="9ed90-238">Eseguire il carico di lavoro di hello esempio OLTP</span><span class="sxs-lookup"><span data-stu-id="9ed90-238">Run hello sample OLTP workload</span></span>

<span data-ttu-id="9ed90-239">l'unica differenza tra i due seguenti hello Hello *stored procedure* che prima procedura hello utilizza le versioni con ottimizzazione per la memoria delle tabelle di hello, hello durante la seconda procedura utilizza tabelle su disco normali hello:</span><span class="sxs-lookup"><span data-stu-id="9ed90-239">hello only difference between hello following two *stored procedures* is that hello first procedure uses memory-optimized versions of hello tables, while hello second procedure uses hello regular on-disk tables:</span></span>

- <span data-ttu-id="9ed90-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="9ed90-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="9ed90-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="9ed90-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="9ed90-242">In questa sezione viene visualizzato come toouse hello utile **ostress.exe** tooexecute utilità hello due stored procedure senza livelli.</span><span class="sxs-lookup"><span data-stu-id="9ed90-242">In this section, you see how toouse hello handy **ostress.exe** utility tooexecute hello two stored procedures at stressful levels.</span></span> <span data-ttu-id="9ed90-243">È possibile confrontare il tempo impiegato per hello due stress esecuzioni toofinish.</span><span class="sxs-lookup"><span data-stu-id="9ed90-243">You can compare how long it takes for hello two stress runs toofinish.</span></span>


<span data-ttu-id="9ed90-244">Quando si esegue ostress.exe, è consigliabile passare valori di parametro progettate per entrambi i seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="9ed90-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of hello following:</span></span>

- <span data-ttu-id="9ed90-245">Eseguire un numero elevato di connessioni simultanee, usando -n100.</span><span class="sxs-lookup"><span data-stu-id="9ed90-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="9ed90-246">Ripetere ogni ciclo di connessione centinaia di volte, usando -r500.</span><span class="sxs-lookup"><span data-stu-id="9ed90-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="9ed90-247">Tuttavia, è consigliabile toostart con valori inferiori come - tooensure n10 e - r50 che funzionino.</span><span class="sxs-lookup"><span data-stu-id="9ed90-247">However, you might want toostart with much smaller values like -n10 and -r50 tooensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="9ed90-248">Script per ostress.exe</span><span class="sxs-lookup"><span data-stu-id="9ed90-248">Script for ostress.exe</span></span>


<span data-ttu-id="9ed90-249">In questa sezione Visualizza script T-SQL hello incorporato della linea di comando ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="9ed90-249">This section displays hello T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="9ed90-250">script di Hello utilizza gli elementi creati da hello script T-SQL che è installato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9ed90-250">hello script uses items that were created by hello T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="9ed90-251">Hello lo script seguente inserisce un ordine di vendita di esempio con cinque voci seguenti hello con ottimizzazione per la memoria *tabelle*:</span><span class="sxs-lookup"><span data-stu-id="9ed90-251">hello following script inserts a sample sales order with five line items into hello following memory-optimized *tables*:</span></span>

- <span data-ttu-id="9ed90-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="9ed90-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="9ed90-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="9ed90-253">SalesLT.SalesOrderDetail_inmem</span></span>


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


<span data-ttu-id="9ed90-254">hello toomake *ondisk* versione di hello precedente script T-SQL per ostress.exe, si devono sostituire entrambe le occorrenze di hello *inmem* substring con *ondisk*.</span><span class="sxs-lookup"><span data-stu-id="9ed90-254">toomake hello *_ondisk* version of hello preceding T-SQL script for ostress.exe, you would replace both occurrences of hello *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="9ed90-255">Queste sostituzioni interessano nomi hello delle tabelle e stored procedure.</span><span class="sxs-lookup"><span data-stu-id="9ed90-255">These replacements affect hello names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="9ed90-256">Installare le utilità RML e ostress</span><span class="sxs-lookup"><span data-stu-id="9ed90-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="9ed90-257">Idealmente, è possibile pianificare toorun ostress.exe in una macchina virtuale di Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="9ed90-257">Ideally, you would plan toorun ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="9ed90-258">Si creerà un [macchina virtuale di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) in hello stessa area geografica Azure in cui risiede il database AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="9ed90-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in hello same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="9ed90-259">È possibile eseguire ostress.exe sul computer portatile.</span><span class="sxs-lookup"><span data-stu-id="9ed90-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="9ed90-260">In hello macchina virtuale o in qualsiasi host è scegliere, installare le utilità di hello riproduzione Markup Language (RML).</span><span class="sxs-lookup"><span data-stu-id="9ed90-260">On hello VM, or on whatever host you choose, install hello Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="9ed90-261">utilità di Hello includono ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="9ed90-261">hello utilities include ostress.exe.</span></span>

<span data-ttu-id="9ed90-262">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="9ed90-262">For more information, see:</span></span>
- <span data-ttu-id="9ed90-263">Hello discussione ostress.exe in [Database di esempio per OLTP In memoria](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed90-263">hello ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="9ed90-264">[Database di esempio per OLTP in memoria](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed90-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="9ed90-265">Hello [blog per l'installazione ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed90-265">hello [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a><span data-ttu-id="9ed90-266">Eseguire hello *inmem* stress prima del carico di lavoro</span><span class="sxs-lookup"><span data-stu-id="9ed90-266">Run hello *_inmem* stress workload first</span></span>


<span data-ttu-id="9ed90-267">È possibile utilizzare un *prompt comandi RML* toorun finestra la riga di comando ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="9ed90-267">You can use an *RML Cmd Prompt* window toorun our ostress.exe command line.</span></span> <span data-ttu-id="9ed90-268">i parametri della riga di comando Hello diretta ostress per:</span><span class="sxs-lookup"><span data-stu-id="9ed90-268">hello command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="9ed90-269">Eseguire 100 connessioni simultaneamente (-n100).</span><span class="sxs-lookup"><span data-stu-id="9ed90-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="9ed90-270">Ogni connessione eseguire script T-SQL hello 50 volte (-r50).</span><span class="sxs-lookup"><span data-stu-id="9ed90-270">Have each connection run hello T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="9ed90-271">hello toorun ostress.exe della riga di comando precedente:</span><span class="sxs-lookup"><span data-stu-id="9ed90-271">toorun hello preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="9ed90-272">Reimpostare il contenuto di dati di hello database tramite l'esecuzione di tutti i dati che è stati inseriti da tutte le esecuzioni precedenti hello hello in SSMS, toodelete comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9ed90-272">Reset hello database data content by running hello following command in SSMS, toodelete all hello data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="9ed90-273">Copiare il testo hello di hello precedente ostress.exe riga di comando tooyour Appunti.</span><span class="sxs-lookup"><span data-stu-id="9ed90-273">Copy hello text of hello preceding ostress.exe command line tooyour clipboard.</span></span>

3. <span data-ttu-id="9ed90-274">Sostituire hello `<placeholders>` per hello parametri -S - U -P -d con hello correggere i valori reali.</span><span class="sxs-lookup"><span data-stu-id="9ed90-274">Replace hello `<placeholders>` for hello parameters -S -U -P -d with hello correct real values.</span></span>

4. <span data-ttu-id="9ed90-275">Eseguire la riga di comando modificata in una finestra dei comandi RML.</span><span class="sxs-lookup"><span data-stu-id="9ed90-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="9ed90-276">Il risultato è un intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="9ed90-276">Result is a duration</span></span>


<span data-ttu-id="9ed90-277">Al termine, ostress.exe scrive hello durata di esecuzione come riga finale di output nella finestra Cmd RML hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-277">When ostress.exe finishes, it writes hello run duration as its final line of output in hello RML Cmd window.</span></span> <span data-ttu-id="9ed90-278">Ad esempio, per un'esecuzione dei test più breve, durata circa 1,5 minuti:</span><span class="sxs-lookup"><span data-stu-id="9ed90-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="9ed90-279">Reimpostare, modificare per l'esecuzione *_ondisk* ed eseguire di nuovo il test</span><span class="sxs-lookup"><span data-stu-id="9ed90-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="9ed90-280">Dopo aver risultato hello hello *inmem* esecuzione, eseguire hello alla procedura seguente per hello *ondisk* eseguire:</span><span class="sxs-lookup"><span data-stu-id="9ed90-280">After you have hello result from hello *_inmem* run, perform hello following steps for hello *_ondisk* run:</span></span>


1. <span data-ttu-id="9ed90-281">Ripristina database hello mediante l'esecuzione di tutti i dati che è stati inseriti da hello precedente esecuzione hello hello in SSMS toodelete comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9ed90-281">Reset hello database by running hello following command in SSMS toodelete all hello data that was inserted by hello previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="9ed90-282">Modifica hello ostress.exe riga di comando tooreplace tutti *inmem* con *ondisk*.</span><span class="sxs-lookup"><span data-stu-id="9ed90-282">Edit hello ostress.exe command line tooreplace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="9ed90-283">Eseguire di nuovo ostress.exe per hello seconda volta e acquisire i risultati di durata hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-283">Rerun ostress.exe for hello second time, and capture hello duration result.</span></span>

4. <span data-ttu-id="9ed90-284">Nuovamente, reimpostare hello (per l'eliminazione in modo responsabile di ciò che può essere una grande quantità di dati di test).</span><span class="sxs-lookup"><span data-stu-id="9ed90-284">Again, reset hello database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="9ed90-285">Risultati previsti per il confronto</span><span class="sxs-lookup"><span data-stu-id="9ed90-285">Expected comparison results</span></span>

<span data-ttu-id="9ed90-286">I test In memoria hanno dimostrato che le prestazioni migliorate **nove volte** per questo carico di lavoro semplice, con ostress in esecuzione in una macchina virtuale di Azure in hello stessa regione di Azure come database hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in hello same Azure region as hello database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a><span data-ttu-id="9ed90-287">2. Installare: esempio hello Analitica In memoria</span><span class="sxs-lookup"><span data-stu-id="9ed90-287">2. Install hello In-Memory Analytics sample</span></span>


<span data-ttu-id="9ed90-288">In questa sezione è confrontare hello IO e risultati delle statistiche quando si utilizza un indice columnstore e un indice albero b tradizionale.</span><span class="sxs-lookup"><span data-stu-id="9ed90-288">In this section, you compare hello IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="9ed90-289">Per analitica in tempo reale in un carico di lavoro OLTP, spesso è migliore toouse un indice columnstore non cluster.</span><span class="sxs-lookup"><span data-stu-id="9ed90-289">For real-time analytics on an OLTP workload, it's often best toouse a nonclustered columnstore index.</span></span> <span data-ttu-id="9ed90-290">Per informazioni dettagliate, vedere [Descrizione degli indici columnstore](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed90-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-hello-columnstore-analytics-test"></a><span data-ttu-id="9ed90-291">Preparare hello columnstore analitica test</span><span class="sxs-lookup"><span data-stu-id="9ed90-291">Prepare hello columnstore analytics test</span></span>


1. <span data-ttu-id="9ed90-292">Utilizzare hello toocreate portale Azure un nuovo database AdventureWorksLT tratto dall'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-292">Use hello Azure portal toocreate a fresh AdventureWorksLT database from hello sample.</span></span>
 - <span data-ttu-id="9ed90-293">Usare esattamente questo nome.</span><span class="sxs-lookup"><span data-stu-id="9ed90-293">Use that exact name.</span></span>
 - <span data-ttu-id="9ed90-294">Scegliere qualsiasi livello di servizio Premium.</span><span class="sxs-lookup"><span data-stu-id="9ed90-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="9ed90-295">Hello copia [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour Appunti.</span><span class="sxs-lookup"><span data-stu-id="9ed90-295">Copy hello [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour clipboard.</span></span>
 - <span data-ttu-id="9ed90-296">Hello script T-SQL hello crea oggetti In memoria necessarie nel database di esempio AdventureWorksLT hello creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="9ed90-296">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="9ed90-297">script di Hello Crea tabella della dimensione hello e due tabelle dei fatti.</span><span class="sxs-lookup"><span data-stu-id="9ed90-297">hello script creates hello Dimension table and two fact tables.</span></span> <span data-ttu-id="9ed90-298">le tabelle dei fatti Hello vengono popolate con 3,5 milioni di righe ognuno.</span><span class="sxs-lookup"><span data-stu-id="9ed90-298">hello fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="9ed90-299">script Hello potrebbe richiedere toocomplete 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="9ed90-299">hello script might take 15 minutes toocomplete.</span></span>

3. <span data-ttu-id="9ed90-300">Incollare lo script T-SQL di hello in SQL Server Management Studio e quindi eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-300">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="9ed90-301">Hello **COLUMNSTORE** parola chiave in hello **CREATE INDEX** istruzione è fondamentale, come in:</span><span class="sxs-lookup"><span data-stu-id="9ed90-301">hello **COLUMNSTORE** keyword in hello **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="9ed90-302">Impostare il livello di toocompatibility AdventureWorksLT 130:</span><span class="sxs-lookup"><span data-stu-id="9ed90-302">Set AdventureWorksLT toocompatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="9ed90-303">Livello 130 non funzionalità memoria tooIn direttamente correlati.</span><span class="sxs-lookup"><span data-stu-id="9ed90-303">Level 130 is not directly related tooIn-Memory features.</span></span> <span data-ttu-id="9ed90-304">ma offre in genere prestazioni delle query più veloci rispetto al livello 120.</span><span class="sxs-lookup"><span data-stu-id="9ed90-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="9ed90-305">Tabelle e indici columnstore fondamentali</span><span class="sxs-lookup"><span data-stu-id="9ed90-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="9ed90-306">dbo. FactResellerSalesXL_CCI è una tabella che include un indice columnstore cluster, che offre avanzati per la compressione a hello *dati* livello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at hello *data* level.</span></span>

- <span data-ttu-id="9ed90-307">dbo. FactResellerSalesXL_PageCompressed è una tabella con un equivalente regolare indice cluster, che è compressi solo a hello *pagina* livello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at hello *page* level.</span></span>


#### <a name="key-queries-toocompare-hello-columnstore-index"></a><span data-ttu-id="9ed90-308">Indice di chiave di query toocompare hello columnstore</span><span class="sxs-lookup"><span data-stu-id="9ed90-308">Key queries toocompare hello columnstore index</span></span>


<span data-ttu-id="9ed90-309">Esistono [diversi tipi di query T-SQL che è possibile eseguire](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee miglioramenti delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9ed90-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee performance improvements.</span></span> <span data-ttu-id="9ed90-310">Nel passaggio 2 in hello script T-SQL, si paga coppia toothis attenzione di query.</span><span class="sxs-lookup"><span data-stu-id="9ed90-310">In step 2 in hello T-SQL script, pay attention toothis pair of queries.</span></span> <span data-ttu-id="9ed90-311">Le due query differiscono per una sola riga:</span><span class="sxs-lookup"><span data-stu-id="9ed90-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="9ed90-312">Un indice columnstore cluster è in hello FactResellerSalesXL\_tabella CCI.</span><span class="sxs-lookup"><span data-stu-id="9ed90-312">A clustered columnstore index is in hello FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="9ed90-313">Hello estratto di script T-SQL seguente stampa le statistiche dei / o e l'ora di query hello di ogni tabella.</span><span class="sxs-lookup"><span data-stu-id="9ed90-313">hello following T-SQL script excerpt prints statistics for IO and TIME for hello query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
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


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
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

<span data-ttu-id="9ed90-314">In un database con livello di prezzo hello P2, è possibile prevedere circa nove volte hello miglioramento delle prestazioni per la query utilizzando l'indice columnstore cluster hello confrontato con un indice tradizionale hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-314">In a database with hello P2 pricing tier, you can expect about nine times hello performance gain for this query by using hello clustered columnstore index compared with hello traditional index.</span></span> <span data-ttu-id="9ed90-315">Con P15, è possibile prevedere miglioramento delle prestazioni di hello circa 57 volte utilizzando l'indice columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="9ed90-315">With P15, you can expect about 57 times hello performance gain by using hello columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="9ed90-316">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9ed90-316">Next steps</span></span>

- [<span data-ttu-id="9ed90-317">Avvio rapido 1: Tecnologie OLTP in memoria per ottimizzare le prestazioni di T-SQL</span><span class="sxs-lookup"><span data-stu-id="9ed90-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="9ed90-318">Usare OLTP in memoria in un'applicazione esistente del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed90-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="9ed90-319">[Monitoraggio dell'archiviazione OLTP in memoria](sql-database-in-memory-oltp-monitoring.md) per OLTP in memoria.</span><span class="sxs-lookup"><span data-stu-id="9ed90-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9ed90-320">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9ed90-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="9ed90-321">Approfondimenti</span><span class="sxs-lookup"><span data-stu-id="9ed90-321">Deeper information</span></span>

- <span data-ttu-id="9ed90-322">[Informazioni in Learn how Quorum doubles key database's workload while lowering DTU by 70% with In-Memory OLTP in SQL Databas](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database) (Il quorum raddoppia il carico di lavoro del database principale riducendo il DTU del 70% con OLTP in memoria nel database SQL)</span><span class="sxs-lookup"><span data-stu-id="9ed90-322">[Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>

- <span data-ttu-id="9ed90-323">[In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/) (Post di blog su OLTP nel database SQL di Azure)</span><span class="sxs-lookup"><span data-stu-id="9ed90-323">[In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

- [<span data-ttu-id="9ed90-324">Informazioni su OLTP in memoria</span><span class="sxs-lookup"><span data-stu-id="9ed90-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="9ed90-325">Informazioni sugli indici columnstore</span><span class="sxs-lookup"><span data-stu-id="9ed90-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="9ed90-326">Informazioni sulle analisi operative in tempo reale</span><span class="sxs-lookup"><span data-stu-id="9ed90-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="9ed90-327">Vedere l'articolo sui [modelli comuni dei carichi di lavoro e considerazioni relative alla migrazione](http://msdn.microsoft.com/library/dn673538.aspx), che descrive modelli di carico di lavoro in cui OLTP in memoria fornisce in genere miglioramenti significativi delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="9ed90-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="9ed90-328">Progettazione di applicazioni</span><span class="sxs-lookup"><span data-stu-id="9ed90-328">Application design</span></span>

- [<span data-ttu-id="9ed90-329">OLTP in memoria (ottimizzazione in memoria)</span><span class="sxs-lookup"><span data-stu-id="9ed90-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="9ed90-330">Usare OLTP in memoria in un'applicazione esistente del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed90-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="9ed90-331">Strumenti</span><span class="sxs-lookup"><span data-stu-id="9ed90-331">Tools</span></span>

- [<span data-ttu-id="9ed90-332">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9ed90-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="9ed90-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="9ed90-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="9ed90-334">SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="9ed90-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
